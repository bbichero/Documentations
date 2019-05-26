Pfsense
------
Managing network throw web UI

Requirement:
```
Host arch: Debian 9.9
1 bridged interface
Parition / disk with more than 20GB
Specs: 2vcpus 2GB RAM
Virtualizer (KVM + libvirt)
ISO image from pfsense
2 public IPv4 (1 public and one other from failover)
Provider: Online
1 MAC addr from Online failover IPv4
```

You must first [prepare VM installation](VM_installation.md)
Then you must [configure Pfsense](Pfsense.md)

After configurer Pfsense, you need to to Setup a LAN network for our VMs,
you must create an attach another NIC to Pfsense VM.   

Define a new network:
```
vi ${LAN_BRIDGE_NAME}.xml
---
<network>
  <name>${LAN_BRIDGE_NAME}</name>
  <bridge name='${LAN_BRIDGE_NAME}' stp='on' delay='0'/>
</network>
---
```

Define it in virsh:
```
sudo virsh net-define ${LAN_BRIDGE_NAME}.xml
```

Start it and auto start it:
```
sudo virsh net-start ${LAN_BRIDGE_NAME}
sudo virsh net-autostart ${LAN_BRIDGE_NAME}
```

Attach new bridge to Pfsense VM:
```
virsh attach-interface pfsense bridge ${LAN_BRIDGE_NAME} --target ${TARGET_NIC_NAME} --mac ${TARGET_NIC_MAC} --model virtio
```

You must connect to Pfsense to create second interface (LAN) and attach it a private network.
You must follow thoses well documented (with picture) [steps](https://trackit.io/installation-of-a-pfsense-server-on-esxi-with-a-dedicated-ip/)
