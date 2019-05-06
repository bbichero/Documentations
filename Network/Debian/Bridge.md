Bridge
------

Recommends:
```
Distribution: Debian stretch
bridge-utils: 1.5-13
Private subnet like 192.168.1.0/24
```

Bridging connection permit to share your internet connectin between multiple computers
You need to create a private network with a private subnet

```
auto ${BRIDGE_NAME}
iface ${BRIDGE_NAME} inet static
	address  ${GATEWAY_PRIVATE_SUBNET}
	netmask  ${NETMASK_PRIVATE_SUBNET}
        bridge_ports none
        bridge_stp off
        bridge_fd 0

        post-up echo 1 > /proc/sys/net/ipv4/ip_forward
        post-up   iptables -t nat -A POSTROUTING -s '${PRIVATE_SUBNET}' -o ${MAIN_INTERFACE} -j MASQUERADE
        post-down iptables -t nat -D POSTROUTING -s '${PRIVATE_SUBNET}' -o ${MAIN_INTERFACE} -j MASQUERADE
```
