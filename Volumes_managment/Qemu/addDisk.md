Images disk managment
------

### Add additional disk to virt VM
Create a new image:   
`qemu-img create -f ${IMAGE_FORMAT} ${IMAGE_PATH}/${IMAGE_NAME}.${IMAGE_FORMAT} ${IMAGE_SIZE}G -o preallocation=full`
*preallocataion full is needed otherwise VM can't see the full space*

Shutdown VM:   
`virsh shutdown ${VM_NAME}`

Attach new image created to VM   
`virsh attach-disk ${VM_NAME} ${IMAGE_PATH}/${IMAGE_NAME}.${IMAGE_FORMAT} ${TARGET_DISK_NAME} --config --cache none`
