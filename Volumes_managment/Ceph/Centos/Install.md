Installation
-----

Enable extra package for EPEL repository:
```
sudo yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
```

Add ceph repository to your yum configuration:
```
cat << EOM > /etc/yum.repos.d/ceph.repo
[ceph-noarch]
name=Ceph noarch packages
baseurl=https://download.ceph.com/rpm-${CEPH_STABLE_RELEASE}/el7/noarch
enabled=1
gpgcheck=1
type=rpm-md
gpgkey=https://download.ceph.com/keys/release.asc
EOM
```

Update repository and install ceph deploy (install ntp and setuptools too):
```
sudo yum update
sudo yum install ceph-deploy ntp ntpdate ntp-doc python-setuptools
```

Create ceph user and assign him a password (no to call if `ceph`) on ALL nodes    
And connect to his account to execute others commands:
```
useradd -d /home/${CEPH_USERNAME} -m ${CEPH_USERNAME}
passwd ${CEPH_USERNAME}
su ${CEPH_USERNAME}
```

Ensure it has sudo privileges:
```
echo "${CEPH_USERNAME} ALL = (root) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/${CEPH_USERNAME}
sudo chmod 0440 /etc/sudoers.d/${CEPH_USERNAME}
```

Generate edsa keypair (only on ceph admin node):
```
ssh-keygen -a 100 -t ed25519 
```

For each node, copy the priviously public key:
```
ssh-copy-id ${CEPH_USERNAME}@${NODE_1_HOSTNAME}
ssh-copy-id ${CEPH_USERNAME}@${NODE_2_HOSTNAME}
...
```

Add ssh config file on ceph admin node:
```
vi ~/.ssh/config
---
Host ${NODE_1_HOSTNAME}
   Hostname ${NODE_1_HOSTNAME}
   User ${CEPH_USERNAME}
Host ${NODE_2_HOSTNAME}
   Hostname ${NODE_2_HOSTNAME}
   User ${CEPH_USERNAME}
---
```

Open port 6789 for monitor and range 6800:7300  for OSDs between nodes    
then saves your rules:
```
sudo service iptables save
```

On each nodes ensute package manager has priority/preferences installed and enabled:
```
sudo yum install yum-plugin-priorities --enablerepo=rhel-7-server-optional-rpms
```
