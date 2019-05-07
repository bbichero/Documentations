VM installation
------

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
