# Wordpress
## Create database user
```
mysql> GRANT ALL PRIVILEGES ON databasename.* TO "wordpressusername"@"localhost" IDENTIFIED BY "password";
mysql> FLUSH PRIVILEGES;
```

## Search and replace in the wordpress database
```
wp search-replace 'http://mysite.org' 'https://mysite.ca' --skip-columns=guid
```

## Add a new wordpress administrator via wp-cli
```
wp user create <name> <email> --role=administrator
```

## Delete a wordpress user via wp-cli
```
wp user delete <id>
```
