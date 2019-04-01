Installation
------

Install recommends package:   
`sudo apt install --no-install-recomends gcc python3-dev python3-pip`

Install virtualenv command from `pip`:   
`pip install virtualenv`

Create environment and install matrix:   
```
mkdir -p ~/synapse
virtualenv -p python3 ~/synapse/env
source ~/synapse/env/bin/activate
pip install --upgrade pip
pip install --upgrade setuptools
pip install matrix-synapse[all]
```

Generate configuration files fro synapse:   
```
cd ~/synapse
python -m synapse.app.homeserver \
    --server-name ${FQDN} \
    --config-path homeserver.yaml \
    --generate-config \
    --report-stats=[yes|no]
```

Start synapse server:   
`synctl start`


If you want to listen to outside of enable tls edit the configuration.   
After each restart check if server logs are good.

### TLS support
Install nginx for reverse proxy requests:   
`sudo apt install --no-install-recommends nginx`

Remove default conf file:   
`sudo rm /etc/nginx/sites-availables/default`

Create configuration (listen on `80` only temporary):   
`sudo vi /etc/nginx/site-available/matrix.conf`

```
server {
    listen 80;
    #listen 443 ssl;
    #listen [::]:443 ssl;
    server_name ${FQDN};

    location /_matrix {
        proxy_pass http://localhost:8008;
        proxy_set_header X-Forwarded-For $remote_addr;
    }
}
```

Download Certbot binary and generate certificates:   
`./certbot-auto --no-bootstrap --nginx -d ${FQDN}`

Remote `listen 80` line and uncomment the 2 following lines.
Restart nginx:   
`sudo systemctl restart nginx`
