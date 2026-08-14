---
id: linux_time
aliases: []
tags:
  - linux
  - commands
---

```
$ stat neumo
  File: neumo
  Size: 4096      	Blocks: 8          IO Block: 4096   directory
Device: 801h/2049d	Inode: 782825      Links: 6
Access: (0750/drwxr-x---)  Uid: (30033/   neumo)   Gid: (30033/   neumo)
Access: 2026-07-04 06:26:20.331010911 +0000
Modify: 2026-07-04 06:13:21.927636638 +0000
Change: 2026-07-04 06:13:21.927636638 +0000
 Birth: 2025-07-05 06:45:27.382513283 +0000
```

- Access: Read the content of the file, e.g., `cat`. But most modern Linux usually don't update `atime` every time the file is read. You can check the current mount option with `findmnt -no TARGET,OPTIONS /path/to/mountpoint`. You will often see `relatime` which means Linux updates `atime` only when necessary: the previous `atime` is older than a certain threshold or the previous `atime` is earlier than `mtime` or `ctime`.
- Modify: Modify the content of the file
- Change: Change the metadata of the file, e.g. `chmod`

`stat` will not update `Access` time because it does not read the content of the file.

On the RTC(Real-Time Clock), Windows saves local time while Linux saves UTC time. That's the cause of dual-boot time mismatch. It's recommended to let Windows use UTC by modifying the registy. On linux, you can check if your system is using RTC in local TZ with `timedatectl`
