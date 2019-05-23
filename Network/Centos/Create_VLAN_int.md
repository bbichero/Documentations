Create VLAN interface
------

Create Vlan interface file:
```
sudo vi /etc/sysconfig/network-scripts/ifcfg-${INT_NAME}.${VLAN_ID}
-----
DEVICE=${INT_NAME}.${VLAN_ID}
BOOTPROTO=static
ONBOOT=yes
IPADDR=${IP_ADDR}
TYPE=Ethernet
NETMASK=${NETMASK_ADDR}
VLAN=yes
-----
```

Restart networking service:
```
sudo systemctl restart networking
```
