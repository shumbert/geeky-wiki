# Apache
## Find list of loaded modules in Apache

Use the following command to list Loaded modules in your Apache/HTTPD server in Linux
```
root@centos [~]# httpd -D DUMP_MODULES
(or)
user@centos [~]# sudo httpd -D DUMP_MODULES
(or)
user@ubuntu [~]# sudo apache2 -D DUMP_MODULES
```

Depending on your Linux distro, you need to use either httpd or apache2. Also use ‘sudo’ if you’re not logged in as root user.

Sample loaded modules in Apache
```
Loaded Modules:
 core_module (static)
 include_module (static)
 proxy_module (static)
 proxy_connect_module (static)
 http_module (static)
 autoindex_module (static)
 info_module (static)
 cloudflare_module (shared)
 php5_module (shared)
 reqtimeout_module (shared)
 pagespeed_module (shared)
Syntax OK
```

## Find list of compiled modules in Apache
Use the following command to list compiled modules in Apache/HTTPD server in Linux

```
root@centos [~]# httpd -l
(or)
user@centos [~]# sudo httpd -l
(or)
user@ubuntu [~]# sudo apache2 -l
```

Depending on your Linux distro, you need to use either httpd or apache2. Also use ‘sudo’ if you’re not logged in as root user.

Sample compiled modules in Apache
```
Compiled in modules:
 core.c
 mod_include.c
 mod_proxy.c
 mod_proxy_connect.c
 mod_proxy_http.c
 http_core.c
 mod_autoindex.c
 mod_info.c
 mod_actions.c
 mod_alias.c
 mod_rewrite.c
 mod_so.c
```
