Set up storage cluster
------
[Official documentation](http://docs.ceph.com/docs/master/start/quick-ceph-deploy)

Requirements:
```
2 Hosts with each:
- 2 x 2To HDD (/dev/sdc, /dev/sdd)
- 2 x 120Gb SSD (/dev/sda, /dev/sdb)
- 1 public net interface
- 1 private connected with other host
```

Create directory for cluster configuration file and go into it:
```
mkdir ${CLUSTER_NAME}
cd ${CLUSTER_NAME}
```

Deploy your first monitor on your admin node:
```
ceph-deploy new ${NODE_1_HOSTNAME}
```

After deploy monitor, you should see a `ceph.conf` file, open it and add `cluster_network` :
```
[global]
...
ms_bind_ipv6 = true
mon_initial_members = ${NODE_1_HOSTNAME}
mon_host = ${PRIVATE_NODE_1_ADDR}
cluster_network = ${PRIVATE_NODE_1_ADDR}/${NETWORK_BIT_LENGHT}
auth_cluster_required = cephx
auth_service_required = cephx
auth_client_required = cephx
...
```

*Ceph do not handle Debian buster in their repository*
*You must install ceph packages manualy*
Install ceph packages on all nodes:
```
sudo apt install ceph-base ceph-common ceph-mds ceph-mgr ceph-mon ceph-osd ceph-resource-agents
```

Deploy the initial monitor and gather the keys:
```
ceph-deploy mon create-initial
```

Copy configuration file and admin key to nodes:
```
ceph-deploy admin ${NODE_1_HOSTNAME} ${NODE_2_HOSTNAME} ...
```

Deploy a manager daemon:
```
ceph-deploy mgr create ${NODE_1_HOSTNAME}
```

OSDs deploy
---
Create volume group with HDD disk:
```
sudo vgcreate ceph-block-0 /dev/sda
```

Create logical volume for block:
```
sudo lvcreate -l 100%FREE -n block-0 ceph-block-0
```

Create Volume group and logical disk for SSD:
```
sudo vgcreate ceph-db-0 /dev/sda
sudo lvcreate -L 15GB -n db-0 ceph-db-0
```

On admin node:
```
ceph-deploy osd create --data /dev/ceph-block-0/block-0 --journal /dev/ceph-db-0/db-0 arch-1
```

MONs deploy (monitors)
---
Add another monitory to cluster:
You must first edit your `ceph.conf` file and add node2 hostname to `mon_host` and to `mon_initial_members`    
then execute:
```
ceph-deploy mon add ${NODE_2_HOSTNAME}
```

Displays monitors:
```
sudo ceph quorum_status --form json-pretty
```

MNGs deploy (managers)
---
If one daemon or host fails, anothers one can take over without interrupting service.   

Add another manager:
```
ceph-deploy mgr create ${NODE_2_HOSTNAME}
```

You should see it with:
```
sudo ceph -s
```

RGWs deploy (object gateway)
---
S3 / swift compatible http api

Deploy rgw:
```
ceph-deploy rgw create ${NODE_1_HOSTNAME}
```
