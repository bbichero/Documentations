How to convert virtualbox VM to Qemu / KVM VM ?
------

Environment:
#### Source host:
```
Distribution: MacOS Sierra 10.12.6
Virtualbox: 5.2.18 r124319
```
#### Destination host:
```
Distribution: Buster/sid
Qemu: QEMU emulator version 3.1.0 (Debian 1:3.1+dfsg-5)
LVM (recommended): 2.03.02(2) (2018-12-18)
```

### Recommended part (LVM):   
Create LVM for the futur VM:   
`sudo lvcreate -L ${DISK_SIZE} -n ${DISK_NAME} ${VOLUME_GROUP_NAME}`

Make a linux `ext4` filesystem:   
`sudo mkfs.ext4 /dev/${VOLUME_GROUP_NAME}/${DISK_NAME}`

Mount it:   
`sudo mount -t ext4 /dev/${VOLUME_GROUP_NAME}/${DISK_NAME} /${MOUNT_PATH}`

Convert `vhd` disk image to `qcow2`
`qemu-img convert -f vpc -O qcow2 ${VM_NAME}.vhd ${VM_NAME}.qcow2`

Create VM from disk:   
```
virt-install --import \
	--name ${VM_NAME} \
	--ram 1024 \
	--disk path=/${MOUNT_PATH}/${VM_NAME}.qcow2 \
	--vcpus 1 \
	--os-type linux \
	--os-variant generic \
	--network bridge=virbr0 \
	--graphics none \ 
	--console pty,target_type=serial
```
