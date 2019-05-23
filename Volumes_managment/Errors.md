Errors
------

When you execute `sudo fdisk -l` and you see:
```
Partition 1 does not start on physical sector boundary.
```

Reason: Your hard disk has Advanced Format 4096-byte sectors to    
		which the partition is not perfectly aligned

You must delete all concerned partions with `fdisk`:
```
sudo fdisk /dev/${CONCERNED_DISK}
d
${NUMBER_PARTITION_CONCERNED}
```
