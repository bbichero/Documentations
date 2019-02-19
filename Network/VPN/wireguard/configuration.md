Wireguard conf
------

After installing wireguard on client and server

### On server
copy conf given and generate public / private key

On your iptables configuration add this lines:
```
# Wg rules
iptables -A FORWARD -i ${wg_net} -j ACCEPT
iptables -A FORWARD -o ${wg_net} -j ACCEPT
iptables -t nat -A POSTROUTING -o ${main_net} -j MASQUERADE
```

Power on interface
`sudo wg-quick up ${wg_net}`

List peer
`sudo wg show`

### On client
Copy cont given and generate public / private key
On your iptable configuration add this lines:

```
# Wg rules
iptables -A INPUT -i ${main_net} -p tcp --dport ${wg_port} -m state --state ESTABLISHED -s ${server_private_ipv4}/32 -j ACCEPT
iptables -A OUTPUT -o ${main_net} -p tcp --sport ${wg_port} -m state --state NEW,ESTABLISHED -d ${server_private_ipv4}/32 -j ACCEPT
```

Power on interface
`sudo wg-quick up ${wg_port}`

List peer
`sudo wg show`

On server if you want to add more peer
`sudo wg set wg0 peer ${client_pub_key} allowed-ips ${client_public_ipv4}/32`

### On server AND client
If you want to route all traffic, active ipv4 forwarding
`sudo vi /etc/sysctl.conf`

```
- #net.ipv4.ip_forward=1
+ net.ipv4.ip_forward=1
```

Enable change
`sysctl -p /etc/sysctl.conf`

Active wireguard interface at boot
`sudo systemctl enable wg-quick@${wg_net}`

For each port you want to be available on client, you must forward packet throw your server
```
iptables -t nat -A PREROUTING -i ${main_net} -p tcp --dport ${server_external_port} -j DNAT --to-destination ${client_wg_ipv4}:${client_internal_port}
iptables -t nat -A POSTROUTING -o ${wg_net} -p tcp --dport ${client_internal_port} -d ${client_wg_ipv4} -j SNAT --to-source ${server_wg_ipv4}

iptables -A FORWARD -i ens2 -o ${wg_net} -p tcp --syn --dport ${client_internal_port} -m conntrack --ctstate NEW -j ACCEPT
```
