# OpenSSL
## Create a self-signed certificate
```
openssl req -x509 -nodes -newkey rsa:4096 -keyout key.pem -out cert.pem -days 3650 -subj '/CN=my.domain'
```

## Generate a strong Diffie-Hellman group
```
sudo openssl dhparam -out /etc/nginx/ssl/dhparam.pem 4096
```
