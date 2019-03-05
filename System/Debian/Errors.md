Errors
------

When executing a sudo command:
```
perl: warning: Setting locale failed.
perl: warning: Please check that your locale settings:
```
You need to define all local env vars, put thoses lines in your `.zshrc` or `.bashrc`
```
export LANGUAGE=en_US.UTF-8
export LANG=en_US.UTF-8
export LC_ALL=en_US.UTF-8
```
Now you need to update change
```
locale-gen en_US.UTF-8
dpkg-reconfigure locales
```

When trying to connect to a remote server throw ssh:
```
Error connection reset by pear : Pearhabs ssh keygen must be regen when creating a new vm
```
Remove all local default ssh keys:
`sudo rm -v /etc/ssh/ssh_host_*`

Reconfigure ssh package
`dpkg-reconfigure openssh-server`

Restart sshd
`sudo systemctl restart restart`

When trying to install vm with `virt-install`:
```
Error on centos 7.3 : qemu-kvm: Failed to create chardev
```
Try to edit `/etc/fstab` file and change disk mount options
```
- devpts		/dev/pts	devpts	defaults	0	0
+ devpts 		/dev/pts 	devpts 	gid=5,mode=620 	0 	0
```

Keyboard do not respond after booting
Edit file `/etc/initramfs-tools/modules` and add
```
hid
usbhid
hid_generic
ohci_pci
```

Update initramfs
`sudo update-initramfs -u`
