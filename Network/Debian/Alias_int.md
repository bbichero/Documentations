Create alias network interface
------

Edit network interface file and add:
```
sudo vi /etc/network/interfaces
------
auto ${NET_NIC}:1
iface ${NET_NIC}:1 inet static
	address ${NET_NIC_ALIAS_IP}
	netmask ${NET_NIC_NETMASK}
	gateway ${NET_NIC_GATEWAY}
------
```

Restart networking service:
```
sudo systemctl restart networking
```
