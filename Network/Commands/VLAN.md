VLAN creation
------

Create interface:
```
ip link add link ${MAIN_INTERFACE} name ${MAIN_INTERFACE}.${VLAN_ID} type vlan id ${VLAN_ID}
ip link set ${MAIN_INTERFACE}.${VLAN_ID} mtu 1400
ip link set dev ${MAIN_INTERFACE}.${VLAN_ID} up
```

Add ipv4 to new interface:
```
ip addr add ${IPV4_RANGE}/24 brd ${IPV4_BROACAST} dev ${MAIN_INTERFACE}.${VLAN_ID}
```
