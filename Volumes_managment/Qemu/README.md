Qemu images
------

### Environment:
General
```
Distribution: Debian buster/sid
Kernel: Linux 4.9.0-4-amd64
```

Packages
```
qemu-img version 3.1.0 (Debian 1:3.1+dfsg-5)
```

### Variables:
#### Global
Name of the VM: (ex: `debian-stretch`)   
`VM_NAME`

Image directory parent full path: (ex: `/home/user/disk`)   
`IMAGE_PATH`

Image format: (ex: `qcow2`)   
`IMAGE_FORMAT`

Disk name *inside* VM: (ex: `vdb`)   
`TARGET_DISK_NAME`

Disk size in Gigabit: (ex: `20`)   
`IMAGE_SIZE`
