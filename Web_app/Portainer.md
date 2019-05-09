Portainer
------
Docker container managment

Requirements:
```
Distribution: Debian sid/buster
Kernel: Linux 4.9.0-9-amd
Portainer: 1.20.2
Docker: 18.09
```

Command to set portainer as a swarm service.    
If you want to manage local docker environment, you need to add this line after the first mount option:   
`--mount type=bind,src=//var/run/docker.sock,dst=/var/run/docker.sock`

Create service:
```
docker service create \
    --name portainer \
	--publish 9000:9000 \
    --replicas=1 \
	--constraint 'node.role == manager' \
    --mount type=bind,src=/${PORTAINER_DATA_PATH},dst=/data \
	portainer/portainer
```

Portainer web UI will be available on port 9000.
