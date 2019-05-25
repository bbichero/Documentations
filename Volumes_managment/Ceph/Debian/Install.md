Installation
-----

Install ceph dependencies from debian repository:
```
sudo apt install ntp ntpdate ntp-doc python-setuptools
```

Add release key from ceph:
```
wget -q -O- 'https://download.ceph.com/keys/release.asc' | sudo apt-key add -
```

Add ceph package repository to apt list:
```
echo deb https://download.ceph.com/debian-luminous/ stretch main | sudo tee /etc/apt/sources.list.d/ceph.list
```

Install ceph deploy:
```
sudo apt install ceph-deploy
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
Install package to save iptables 
```
sudo apt install iptables-persistent
```

Save your rules:
```
sudo dpkg-reconfigure iptables-persistent
```
