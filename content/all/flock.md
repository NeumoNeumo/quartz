---
id: flock
aliases: []
tags:
  - linux
---

- An inode can have multiple open file descriptions (OFD).
- An OFD may be referenced by multiple `fd`s.
- `fork` and `dup` will share the same OFD with its parent.
- `open` will create a new file description.
- `flock` establishes a lock on the file/inode, and the lock is owned by / associated with the open file description.

Example:
```bash
# The following works since fd 8 and fd 9 share the same OFD, thus referring to the same lock ownership
exec 9>/tmp/my.lock
exec 8>&9
flock -n 9
flock -n 8

# The following does not work
exec 9>/tmp/my.lock
exec 8>/tmp/my.lock
flock -n 9
flock -n 8
```

