Errors
------

When adding new monitor with command:
```
ceph-deploy mon create ${NODE_HOSTNAME}
```

```
[${NODE_HOSTNAME}][WARNIN] monitor ${NODE_HOSTNAME} does not exist in monmap
[${NODE_HOSTNAME}][WARNIN] neither `public_addr` nor `public_network` keys are defined for monitors
[${NODE_HOSTNAME}][WARNIN] monitors may not be able to form quorum
```

You must check your `ceph.conf` file, you must have:
```
mon_initial_members =
mon_host =
public_network =
```

An example:
```
[global]
fsid = 33cb5c76-a685-469e-8cdd-fee7c98c3f4d
mon_initial_members = ceph1,ceph2
mon_host = 192.168.61.39,192.168.61.40
auth_cluster_required = cephx
auth_service_required = cephx
auth_client_required = cephx
filestore_xattr_use_omap = true
public_network = 192.168.61.0/24
```

Then execute your command with a rewrite conf argument:
```
ceph-deploy --overwrite-conf mon create ${NODE_HOSTNAME}
```
