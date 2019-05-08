Attach new network interface
------

After creating a new network with `virsh net-define` we need to create    
a new network card inside VM.    

Attach network to VM (VM must be started):
```
sudo virsh attach-interface ${VM_NAME} ${NETWORK_TYPE} ${NETWORK_NAME} --target ${NET_NIC_NAME} --mac ${MAC_ADDR} --model ${NIC_MODEL}
```
