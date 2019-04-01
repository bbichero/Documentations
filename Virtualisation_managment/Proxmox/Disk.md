Disk managment
------

Environment:
```
LVM: 2.02.168
Partition: home, root, swap
```

### Resize disks
#### On proxmox host:
Shutdown VM and enter image directory:   
`cd /var/lib/vz/images/${VM_UID}`

Resize image:   
`sudo qemu-img resize vm-${VM_UID}-disk.qcow2`

#### On proxmox guest:
Install `parted` package:   
`sudo apt install parted`

Connect to VM and resize partition:   
`sudo parted /dev/${LOCAL_DISK_NUMERb}`

List partitions and find yours:
`list`

Resize it and quit `parted`:   
```
resizepart ${PARTITION_NUMBER}
q
```

Resize physical volume:   
`sudo pvresize /dev/${LOCAL_DISK_NUMBER}`

Resize logical volume (done on umount partition):   
`sudo lvresize /dev/${LVM_PARTITION_PATH} -l 100%VG`

Resize filesystem (done on umount partition):   
`sudo resize2fs /dev/${LVM_PARTITION_PATH}`
