Create VLAN interface
------

Create Vlan interface file, you must append:
```
sudo vi /etc/network/interface
-----
auto ${INT_NAME}.${VLAN_ID}
iface ${INT_NAME}.${VLAN_ID} inet static
  address ${IP_ADDR}
  netmask ${NETMASK_ADDR}
  vlan-raw-device ${VLAN_ID}
  mtu 1400
-----
```

Restart networking service:
```
sudo systemctl restart networking
```
