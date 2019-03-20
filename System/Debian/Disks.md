Disk documentaions and errors resolution
------

Can't umount busy target disk:
```
umount: /${DISK_PATH}: target is busy
```
Make a lazy umount, detach filesystem from file herarchy
`sudo umount -l /${DISK_PATH}`

If you got error:
```
cannot remove '..': Read-only file system
```
There is a problem with the root system, you must remount it:
`sudo mount -o remount /`
