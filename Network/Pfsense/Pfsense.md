Pfsense configuration
------

First you need to configure interface.   
Let default value and do not configure VLAN right now

Then set interface IP,   
IPv4: ${YOUR_FAILOVER_OPV4}   
NETMASK: 31   
Gateway: BLANK

Now enter in a shell and execute following commands:   
`62.210.0.1` is the default gateway of Online provider.
```
route del default
route add -net 62.210.0.1/32 -iface ${VM_INT_NAME}
route add default 62.210.0.1
```

Test connectivity:
```
ping 1.1.1.1
```

Then while connected to internet you should install shellcmd from pfSense package manager   
and add your gateway there, to get it preserved after a reboot.

In command field, type:
```
route add -net 62.210.0.1/32 -iface ${VM_INT_NAME} && route add default 62.210.0.1
```

Restart Pfsense to assure everything works

After editing a lot of settings, you can export it in case of   
Go to `Diagnostics` => `Backup and Restore` => `Download configuration as XML`
