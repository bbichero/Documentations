Firefox send
------

_Share file with everyone_

Environment:
```
Distribution: Debian 9.8
Kernel: Linux 4.9.0-8-amd64
```

Clone git repository and checkout to last release:   
```
git clone https://github.com/mozilla/send.git
cd clone
git checkout ${LAST_RELEASE}
```

Install nodejs (as root):   
```
curl -sL https://deb.nodesource.com/setup_11.x | bash -
apt-get install -y nodejs
```

Install recommend package for npm install:   
`sudo apt install g++ make`

Install node dependencies:   
`npm install --production`
