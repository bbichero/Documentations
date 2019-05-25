Installation
------

### On ceph admin node
On cluster creation directory (home from `ceph-user`), edit `ceph.conf`:
```
vi ceph.conf
------
[mon.${HOSTNAME_NODE_1}]
       host = ${HOSTNAME_NODE_1}
       mon addr = ${IP_NODE_1}:6789
[mon.${HOSTNAME_NODE_2}]
       host = ${HOSTNAME_NODE_2}
       mon addr = ${IP_NODE_2}:6789
------
```

### On 2 nodes

Install ganeti packages:
```
sudo apt install ganeti
```

Configure hosts files:
```
sudo vi /etc/hosts
------
${IP_NODE_1}	${HOSTNAME_NODE_1} ${HOSTNAME_NAME_1}.${DOMAIN_NAME_NODE_1}
${IP_NODE_2}	${HOSTNAME_NODE_2} ${HOSTNAME_NAME_2}.${DOMAIN_NAME_NODE_2}
${IP_CLUSTER}	${HOSTNAME_CLUSTER} ${HOSTNAME_CLUSTER}.${DOMAIN_NAME_CLUSTER}
------
```
(For this example Cluster IP must be that same as node 1)

Configure network bridge:
```

```

### On ganeti admin node

Initialize cluster
```
sudo gnt-cluster init -d --master-netdev=br0 --enabled-hypervisors=kvm --no-etc-hosts --hypervisor-parameters kvm:initrd_path=,kernel_path=,vhost_net=true,cpu_type=host --enabled-disk-templates=rbd --ipolicy-disk-templates=rbd -D rbd:access=userspace ganeti-cluster
```

Add node 2:
```
```

On node 2, open port 1811
