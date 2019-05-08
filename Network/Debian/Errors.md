Errors
------

```
“RTNETLINK answers: File exists” when running ifup
```

You need to flush network device before `ifup` and `ifdown`   
```
sudo ip addr flush dev ${NET_INT}
```

When creating a virsh network, at network start you got:
```
error: Failed to start network NETWORK_NAME
error: The name org.fedoraproject.FirewallD1 was not provided by any .service files
```

You just need to restart libvirt (no explaination found)
```
sudo systemctl restart libvirtd
sudo virsh net-start NETWORK_NAME
```
