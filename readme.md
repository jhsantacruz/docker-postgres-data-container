# Postgres Data-only Docker Container
This image is used to create a data-only container for Postgres.

1. Start the data-only container as:
``` bash
docker create --name postgres_data jsantacruz/postgres-data-container
```

To use mount to container
``` bash
docker run --volumes-from postgres_data --name postgresdb -e POSTGRES_USER=user -e POSTGRES_PASSWORD=password -d postgres
```
Backups
``` bash
docker run --rm --volumes-from postgres_data -v $(pwd):/backup ubuntu tar cvf /backup/backup.tar /var/lib/postgresql/data
```

Restore
un-tar the backup file
``` bash
docker run --rm --volumes-from postgres_data -v $(pwd):/backup ubuntu bash -c "cd /dbdata && tar xvf /backup/backup.tar --strip 1"
```




example
``` bash
docker create --name pickem-postgres -v /var/lib/postgresql/data postgres:9.4.5
docker create --name pickem-redis -v /var/lib/redis/data redis:3.0.5
```