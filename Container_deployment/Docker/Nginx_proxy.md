Nginx reverse proxy
------

Requirements:
```
Distribution: Debian sid/Buster
Kernel: Linux 4.9.0-9-amd
Docker: 18.09.06
Docker-gen: 0.7.3
```

Download and untar docker-gen file:
```
wget https://github.com/jwilder/docker-gen/releases/download/0.7.3/docker-gen-linux-amd64-0.7.3.tar.gz
tar xvzf docker-gen-linux-amd64-0.7.3.tar.gz
```

Move it to bin folder (or in your `PATH`):
```
sudo mv docker-gen /usr/local/bin/
```
