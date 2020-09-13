# Permissions
## Super laxed permissions
All files in the webroot are owned by the user running the webserver (www-user), or the php interpreter if using php-fpm:
```
chown -R www-user:www-user /path/to/webroot/
find /path/to/webroot -type f -exec chmod 0644 {} \;
find /path/to/webroot -type d -exec chmod 0755 {} \;
chmod 0600 /path/to/webroot/wp-config.php
```


## Laxed permissions
Files are owned by user. User running the webserver (www-user) has only read access to the webroot except for the wp-content folder:
```
chown -R user:user /path/to/webroot/
chown -R user:www-user /path/to/webroot/wp-content/
find /path/to/webroot -type f -exec chmod 0644 {} \;
find /path/to/webroot -type d -exec chmod 0755 {} \;
find /path/to/webroot/wp-content -type f -exec chmod 0664 {} \;
find /path/to/webroot/wp-content -type d -exec chmod 0775 {} \;
chmod 0600 /path/to/webroot/wp-config.php
```

**note:** as the webserver does not have full read/write access, wordpress core auto-update as well as wordpress core update via the web admin interface won't work. Update wordpress core via wp-cli.

**note:** wordpress won't be able to create/update .htaccess files (required when changing the permalink configuration)

## Strict permissions
Files are owned by user. User running the webserver (www-user) has only read access to the webroot except for the wp-content/uploads folder:
```
chown -R user:user /path/to/webroot/
chown -R www-user:www-user /path/to/webroot/wp-content/uploads
find /path/to/webroot -not -perm 0644 -type f -exec chmod 0644 {} \;
find /path/to/webroot -not -perm 0755 -type d -exec chmod 0755 {} \;
chmod 0600 /path/to/webroot/wp-config.php
```

**notes:** all updates (core/plugins/themes) have to be done via wp-cli, themes cannot be edited from the web interface.
