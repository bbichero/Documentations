Wireguard
------

### Environment:
General
```
Distribution: Debian stretch
Kernel: Linux 4.9.0-8-amd64
```

Packages
```
Wireguard: 0.0.20181018-1
```

**privates ipv4 are only used if server and client are in the same private network**
If it's not the case replace with public IPv4

### Variables:
#### Global
Name of the wireguard network interface   
`wg_net`

Name of the main network interface (with public ipv4)   
`main_net`

Listen port for wiregard server service   
`wg_port`

Client IPv4 to communique with server
`client_private_ipv4`

Server IPv4 to communique with client   
`server_private_ipv4`

Client public key   
`client_pub_key`

Wireguard server IPv4   
`server_wg_ipv4`

Wireguard client IPv4   
`client_wg_ipv4`

DNS ipv4 used by resolver
`dns_ipv4`

#### Port forwarding
External use by client to receive connection   
`server_external_port`

Internal port on which client will receive connection   
`client_internal_port`
