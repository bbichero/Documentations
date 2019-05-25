Commands
------

To edit ceph configuration, edit first on admin node the `ceph.conf`, then deploy it to all others nodes:
```
ceph-deploy --overwrite-conf admin ${NODE_1_HOSTNAME}
ceph-deploy --overwrite-conf admin ${NODE_2_HOSTNAME}
```
