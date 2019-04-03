Debops
------

Environment:
```
Linux Release: Debian stretch 8.9
Kernel version: linux 4.9 amd64
Ansible: 2.7.9
Debops: 0.8.1
Debops project path: ~/${VIRTUALENV_NAME}
```

Install mandatory packages:   
`sudo apt install gcc python3-pip libldap2-dev libsasl2-dev`

Create virtualenv and source it:
```
virtualenv -p python3 ~/${VIRTUALENV_NAME}
cd ~/${VIRTUALENV_NAME}
source bin/activate
```

Install `debops` and `ansible` with pip:   
`pip install debops[ansible]`

Initialize Debops projet:   
`debops-init .`
