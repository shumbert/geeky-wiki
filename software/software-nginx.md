# Configuration generator
Digital Ocean has an [nginx configuration generator](https://www.digitalocean.com/community/tools/nginx).

# Benchmarking
Use Apache Benchmark for benchmarking (https://httpd.apache.org/docs/2.4/programs/ab.html). On debian install it with:
```
sudo apt install apache2-utils
```

Then run with:
```
ab -c10000 -n50 https://example.com
```

# Wordpress configuration
## Core
```
location / {
  index index.php index.html index.htm;
  # Last target of try_files directive is required for permalinks
  try_files $uri $uri/ /index.php?$args;
}

location ~ /\. {
  deny all;
}

location ~* ^/wp-content/uploads/.*.(html|htm|shtml|php|js|swf)$ {
    deny all;
}

location ~* wp-config.php {
    deny all;
}
```

## Configuration for akismet plugin
```
location ~ \.php$ {
  fastcgi_pass            unix:/run/php/php7.0-fpm.sock;
  try_files               $uri =404;
  fastcgi_split_path_info ^(.+\.php)(/.+)$;
  fastcgi_index           index.php;
  fastcgi_read_timeout    300;
  include                 fastcgi.conf;
}
```

## Wordpress plugins
Some wordpress plugins include an .htaccess file. As nginx does not support those, the .htaccess has to be translated and incorporated in the main nginx configuration file.
