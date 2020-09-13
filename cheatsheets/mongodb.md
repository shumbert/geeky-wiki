# MongoDB
## Mongo shell
Start the mongo shell using:
```
mongo
```

### List databases
```
show dbs
```

### Use a database
```
use <db>
```

### List collections
```
show collections
```

## Quit
```
quit()
```

## Backup a database
```
mongodump --db <db> --out /path/to/dump/
```

## Restore a database
```
mongorestore /path/to/dump/
```
