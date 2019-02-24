Errors
------

### NFS service
When executing: `exportfs -a`
```
exportfs: ${NFS_CLIENT_IP}:/exports: Function not implemented
```
It's mean that nfs isn't start, you need to execute
`sudo systemctl start nfs`
