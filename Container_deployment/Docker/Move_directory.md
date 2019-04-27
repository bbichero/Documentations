Move docker directory
------

Stop docker:
```
sudo systemctl stop docker
```

Copy all data in it:
```
sudo mv /var/lib/docker ${NEW_DIRECTORY_PATH}
```

To change docker data directory, you must edit `/etc/docker/daemon.json` file:
```
sudo vi /etc/docker/daemon.json
```

Edit line:
```
    "graph": "/var/lib/docker",
```

With a new path:
```
    "graph": "${NEW_DIRECTORY_PATH}",
```

Start docker:
```
sudo systemctl start docker
```
