Disk documentaions and errors resolution
------

Can't umount busy target disk:
```
umount: /${DISK_PATH}: target is busy
```
Make a lazy umount, detach filesystem from file herarchy
`sudo umount -l /${DISK_PATH}`
