# Certbot commands
## Obtain and install certificate
```
certbot run
```

## Obtain a new certificate, but do not install it
```
certbot certonly --webroot -w /var/www/domain1.com -d domain1.com -w /var/www/domain2.com -d domain2.com
```

## Obtain certificates (one cert per domain)
```
certbot certonly --webroot -w /var/www/domain1.com -d domain1.com
certbot certonly --webroot -w /var/www/domain2.com -d domain2.com
```

## List certificates
```
certbot certificates
```

## Renew certificates
```
certbot renew
certbot renew --post-hook "systemctl reload nginx"
```

## Force renewal
```
cerbot renew --force-renewal
```

## Revoke certificate
```
certbot revoke --cert-path /etc/letsencrypt/live/CERTNAME/cert.pem
```

# Nginx server block for Letsencrypt http challenge
```
server {
    listen 80 default_server;

    location ^~ /.well-known/acme-challenge/ {
        default_type "text/plain";
        root         /var/www/letsencrypt;
    }

    location = /.well-known/acme-challenge/ {
        return 404;
    }
}
```
