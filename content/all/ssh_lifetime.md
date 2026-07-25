---
id: ssh_lifetime
aliases: []
tags:
  - linux
  - ssh
  - pam
---

```text
systemd                                                      < root
  ├─sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups  < root
  │   └─sshd: username [priv]                                < root
  │       └─sshd: username@pts/0                             < user
  │           └─-fish                                        < user
  │               └─ other commands                          < user
  └─systemd --user                                           < user
      ├─(sd-pam)                                             < user
      └─other services                                       < user
```

1. A root process `sshd` listens on the configured port (usually 22). Upon connection, it forks a child.
2. This child becomes a privileged monitor process, `sshd: <username> [priv]`, to handle cleanup and audit logs.
3. The monitor forks a net-child that handles network traffic, key exchange, and packet parsing as a sandbox user (usually `sshd`).
4. The net-child sends authentication requests to the monitor. When `UsePAM yes`, the monitor runs PAM auth/account (`/etc/pam.d/sshd`) as root.
5. The monitor then calls PAM session to setup the session during which it invokes `pam_systemd.so`.
6. `systemd-logind` maintains its own database in `/run/systemd/sessions`, creates/updates the session scope and asks PID 1 (system-level systemd) to fork a `user@<uid>.service` if it is not running.
7. Since `user@.service` is configured with `PAMName=systemd-user`, this new service process initializes the PAM stack (`/etc/pam.d/systemd-user`) to gather environment variables and limits, etc.
8. To keep the PAM session alive independent of the service payload, the service process creates a `(sd-pam)` helper, whose main purpose is to wait for the service to end and then call `pam_close_session`.
9. The service process sets its UID to the user and `exec`s the `systemd --user` binary, carrying the PAM-generated environment variables. (This explains why we need `(sd-pam)`: after `exec`ing the binary, the process that knew how to run `pam_close_session()` is gone.)
10. Back at step 5, after the session setup phase, the monitor creates an unprivileged new process, `sshd: <username>@pts/N`. This process prepares the user context, establishes the `pty` as the controlling terminal and connects stdin/out/err to it and finally `exec`s run the user's shell.
11. When the user logs out, the ssh monitor detects via `SIGCHLD`. The monitor performs the final cleanup (possibly recording logout time in `wtmp`, removing `utmp` entry, and tearing down the `PTY`).

**Note**: There is a terminology overload on the word `session`. The POSIX session (kernel session) is used to manage all the processes belonging to a specific terminal. It can be set using `setsid` by the process itself. On the other hand, the PAM session in `pam_open_session` mainly concerns environment and policy management for the convenience of the admin. (Read the following section if you don't understand.)
