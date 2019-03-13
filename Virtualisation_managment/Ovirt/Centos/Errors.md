Errors
------

### NFS service
When executing: `exportfs -a`
```
exportfs: ${NFS_CLIENT_IP}:/exports: Function not implemented
```
It's mean that nfs isn't start, you need to execute
`sudo systemctl start nfs`

### Virsh CLI
Libvirt ask user and admin password
```
Please enter your authentication name: 
Please enter your password:
error: failed to connect to the hypervisor
error: authentication failed: authentication failed
```

You need to create special user for sasl   
`saslpasswd2 -a libvirt $(whoami)`
