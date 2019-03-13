Ovirt installation
------
Requirement
```
2 serveurs:
- ovirt-engine (front and backend to manage infrastruture): 
With a minimum of 4GB of ram and 2 vCPU
- ovirt-host (for virtualize machines)
With a minimum of 4GB or ram and 4 vCPU
A third server can be used to host NFS cluster
```

General
```
Distribution: Centos 7.4
Kernel: linux 4.20
```

Packages
```
ovirt: 3.4
nfs: 1.3
cockpit: 176.4
```

Installation
------
### Ovirt-engine installation
Add official repository of ovirt and update   
```
yum install http://resources.ovirt.org/pub/yum-repo/ovirt-release43.rpm
yum update
```

Install ovirt-engine package   
`yum install ovirt-engine`

Configure ovirt   
`engine-setup`

You can use default settings for all question except this one:   
`Host fully qualified DNS name of this server []:`   
Enter your FQND (if not in `/etc/hosts`) or enter your public IPv4

Then you can access you admin panel to: `https://${FQDN}`

### Ovirt-host installation
Add official repository of ovirt
```
yum install http://resources.ovirt.org/pub/yum-repo/ovirt-release43.rpm
yum update
```

Configuration
------
### Add host
On engine host admin panel you must follow theses steps:   
- Click on compute then hosts
- Click on 'New' button for configure your first host
- Configure a name, a hostname, tick ssh_key
- Copy public ssh key to ovirt-host ssh auth key (`/root/.ssh/authorized_keys`)
- Click 'Ok' button then go event page
`ovirtmgmt` network interface can not be present on ovirt-host, so you need to configure it
- Click on the concerned host then go to network interface section
- Click on 'Setup host Network' then drag and drop `ovirtmgmt interface in correct place`
![ovirt-interface](https://gitlab.com:bbichero/Documentation.git/Virtualisation_managment/Ovirt/assets/ovirtmgmt-interface.png)

### Add storage
Storage must be on another server than engine and host in a good environment   
But you can install it along ovirt-engine.
NFS will be the storage type used here (ovirt handle more)

#### NFS server
Install NFS package   
`yum -y install nfs-utils`

Enable and start service
```
systemctl enable nfs-server.service
systemctl start nfs-server.service
systemctl start nfs
```

Create the group kvm   
`groupadd kvm -g 36`

Create user vdsm in group `kvm`   
`useradd vdsm -u 36 -g 36`

Create exports directory for host's vm
```
mkdir /exports
mkdir /exports/data
mkdir /exports/export
mkdir /exports/iso
```
Set the ownership of your exported directories to 36:36, which gives vdsm:kvm ownership
```
chown -R 36:36 /exports/data
chown -R 36:36 /exports/export
chown -R 36:36 /exports/iso
```

Set directory mode
```
chmod 0755 /exports/data
chmod 0755 /exports/export
chmod 0755 /exports/iso
```

NFS use a file placed in `/etc/exports` to list mounted volumes   
Fill file with:
```
/exports        ${NFS_CLIENT_IP}(rw,sync,no_root_squash,no_subtree_check)
```

Each time you edit the files you must run   
`exportfs -a`

After this listed volumes will be available for clients

#### NFS client
Install NFS package   
`yum -y install nfs-utils`

Create destination directory for NFS serveur mounted volumes   
`mkdir /exports`

Mount remote directory   
`mount ${NFS_SERVER_IP}:/exports /exports`
