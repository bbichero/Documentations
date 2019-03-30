Let's encrypt
------

Environment:
```
Distribution: Debian 9.8
Kernel: 4.9.0-8-amd64
```

Install required packages:   
`sudo apt install --no-install-recommends python-virtualenv python-certbot-nginx `

Get certbot binary and chomd it:   
```
wget https://dl.eff.org/certbot-auto
chmod a+x ./certbot-auto
```

Before executing cerbot command make sure your website is public (listen to `0.0.0.0`)

Execute certbot binary for generating certificats:   
`sudo certbot --nginx -d ${HOSTNAME}.${DOMAIN_NAME}`

Certbot will ask you some question, email, validate CGU and give your email to a third part Non-profit entreprise
