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

### VM installation
Create bridge interface on Host:
Replace local internefaces configuration (except for `lo`):
```
vi /etc/network/interfaces
---
# The primary network interface
allow-hotplug ${MAIN_NETWORK_INT}
iface ${MAIN_NETWORK_INT} inet static

auto ${BRIDGE_NAME}
iface ${BRIDGE_NAME} inet static
	address ${PUBLIC_HOST_IPV4}
	gateway ${PUBLIC_HOST_GATEWAY}
	netmask ${PUBLIC_HOST_NETMASK}
	brodcast ${PUBLIC_HOST_BROADCAST}
	bridge_ports ${MAIN_NETWORK_INT}
---
```

Restart network:
```
sudo /etc/init.d/networking restart
```

Create logical volume with LVM and create filesystem:
```
sudo lvcreate -L25G -n pfsense-disk ${VOLUME_GROUP_NAME}
sudo mkfs.ext4 /dev/${VOLUME_GROUP_NAME}/pfsense-disk
```

Mount volume:
```
mount -t ext4 /dev/${VOLUME_GROUP_NAME}/pfsense-disk /${MOUNT_LOATION}/pfsense-disk
```

Download Pfsense ISO image from [official website](https://www.pfsense.org/download/)

Create Virtual machine:
(Size is not exactly the same as LV created, filesystem itself take space)
```
sudo virt-install --name pfsense \
	--ram ${RAM_SIZE} \
	--vcpus=${VCPU_NUMBER} \
	--cdrom=${PFSENSE_ISO_LOCATION} \
	--network=bridge=${BRIDGE_NAME},model=virtio \
	--disk path=/${MOUNT_LOCATION}/pfsense-disk/vm.qcow2,size=24.5 \
	--graphics vnc,port=5999 \
	--console pty,target_type=serial
```

Connect to VNC and [configure Pfsense](Pfsense.md)

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
