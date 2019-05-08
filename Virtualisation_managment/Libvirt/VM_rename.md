VM rename
------

rename virtual machine
```
sudo virsh dumpxml ${VM_NAME} > ${VM_NAME}.xml
```

Edit name property between `<name>` in file, then:
```
sudo virsh undefine ${VM_NAME}
sudo define ${VM_NAME}.xml
```

Restart VM:
```
virsh shutdown ${NEW_VM_NAME}
virsh start ${NEW_VM_NAME}
```
