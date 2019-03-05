Errors
------

When trying to install vm with `virt-install`:
```
Error on centos 7.3 : qemu-kvm: Failed to create chardev
```
Try to edit `/etc/fstab` file and change disk mount options
```
- devpts		/dev/pts	devpts	defaults	0	0
+ devpts 		/dev/pts 	devpts 	gid=5,mode=620 	0 	0
```
