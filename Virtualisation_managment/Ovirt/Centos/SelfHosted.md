SelfHosted
------

Install Ovirt using Cockpit, it will be installed as a VM in a physical host
You need:
- Centos >= 7.5
- A valid FQDN for Cockpit interface.
- A valid FQDN for oVirt engine
- 2 public IPv4 OR 2 private IPv4

Update repositories:
```
sudo yum update -y
```

Add official oVirt repository:
```
sudo yum install https://resources.ovirt.org/pub/yum-repo/ovirt-release43.rpm
```

Install Cockpit and cockpit ovirt dashboard:
```
sudo yum install cockpit cockpit-ovirt-dashboard -y
```

Enable Cockpi:
```
sudo systemctl enable --now cockpit.socket
```

Open firewall:
```
sudo firewall-cmd --add-service=cockpit
sudo firewall-cmd --add-service=cockpit --permanent
```

Go in your browser to: `https://${FQDN}:9090`
You must accept the certificate and login with the root account

Click under the Hosted Engine option.
Before starting you must have a valid `/etc/hosts` and a storage ready with at least 60GB available

`/etc/host` file:
```
127.0.0.1	localhost

${PUBLIC_IPV4}	${FQDN_HOST}	${ALIAS}
${PUBLIC_IPV4}	${FQDN_ENGINE}	${ALIAS}
```
You can replace `PUBLIC` with a private IPv4 but you need to own the subnet and have accees to it.

### Storage

NFS storage if the simpliest 

### Maintenance
[OFFICAL TROUBLESHOOTING](https://www.ovirt.org/documentation/self-hosted/chap-Troubleshooting.html)

If you got problem with the oVirt engine VM, you can manualy restart it or access it throw your host.
First set your engine in maintenance:
```
hosted-engine --set-maintenance --mode=global
```

Restart engine:
```
hosted-engine --vm-shutdown
hosted-engine --vm-start
```

Access to console:
```
hosted-engine --console
```
