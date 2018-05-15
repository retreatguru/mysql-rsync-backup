Fast MySQL backup using rsync
=============================

This is a really bad way to backup MySQL databases, but it's really fast.

It is only suitable for development and testing environments that you want to
reset to an initial state very quickly.

If MySQL is running while backup or restore are running, the DB may end up
in an inconsistent state.

Sample `docker-compose.yml` file to get you going:

```
version: '2'
services:
  db:
    image: mysql:5.7
    volumes:
      - mysql_data:/var/lib/mysql
  backup:
    image: retreatguru/mysql-rsync-backup
    volumes:
      - mysql_data:/var/lib/mysql
      - mysql_data_backup:/var/lib/mysql-backup
volumes:
  mysql_data:
  mysql_data_backup:
```

To backup the data:

```
$ docker-compose exec backup backup-mysql
```

To restore to the last backup:

```
$ docker-compose exec backup restore-mysql
```
