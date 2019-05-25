Ceph
------

### Environment:
General
```
Distribution: Debian 10
Kernel: Linux 4.9.0-9-adm64
```

Packages
```
ceph version 12.2.11
```

Configure `/etc/hosts` files:
```
${IP_NODE_1}	${HOSTNAME_NODE_1}.${DOMAIN_CLUSTER}	${HOSTNAME_NODE_1}
${IP_NODE_2}	${HOSTNAME_NODE_2}.${DOMAIN_CLUSTER}	${HOSTNAME_NODE_2}
```

### Variables:
#### Global

Addresse IPv4 / v6 of first node:   
`IP_NODE_1`

Hostname of first node:   
`HOSTNAME_NODE_1`

Domain name of cluster:   
`DOMAIN_CLUSTER`

`/etc/hosts` file example:
```
192.168.1.1		node1.example.com	node1
192.168.1.2		node2.example.com	node2
```
