Iptables
------

### Environment:
General
```
Distribution: Centos 7.6
Kernel: Linux 3.10.0-957.10.1.el7.x86_64
```

Packages
```
iptables v1.4.21
```

### Remove firewall
Now Centos 7 use firewalld instead of iptables, if you want iptables back, you need:    

Disable firewalld:
```
sudo systemctl disable firewalld
```

Install and enable iptables service:
```
sudo yum install iptables-services
sudo systemctl enable iptables
```

After applying your iptables commandes, save your rules:
```
sudo service iptables save
```
