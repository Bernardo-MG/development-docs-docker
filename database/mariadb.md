# MariaDB

```text
# -----------------------------------------------------------------------------
# BUILD STAGE
# -----------------------------------------------------------------------------
FROM mariadb:latest as build

# That file does the DB initialization but also runs mysql daemon, by removing the last line it will only init
RUN ["sed", "-i", "s/exec \"$@\"/echo \"not running $@\"/", "/usr/local/bin/docker-entrypoint.sh"]

# needed for initialization
# ENV MYSQL_ROOT_USER=demodb
ENV MARIADB_ROOT_PASSWORD=root
ENV MYSQL_USER=demodb
ENV MYSQL_PASSWORD=demodb
ENV MARIADB_DATABASE=demodb

COPY demo_db.sql /docker-entrypoint-initdb.d/

# Need to change the datadir to something else that /var/lib/mysql because the parent docker file defines it as a volume.
# https://docs.docker.com/engine/reference/builder/#volume :
#       Changing the volume from within the Dockerfile: If any build steps change the data within the volume after
#       it has been declared, those changes will be discarded.
RUN ["/usr/local/bin/docker-entrypoint.sh", "mysqld", "--datadir", "/initialized-db", "--aria-log-dir-path", "/initialized-db"]

# -----------------------------------------------------------------------------
# DEPLOYMENT STAGE
# -----------------------------------------------------------------------------
FROM mariadb:latest

COPY --from=build /initialized-db /var/lib/mysql
```

## Case Insensitive

```text
services:
    database:
        build: ./database
        container_name: demodb
        command: --lower_case_table_names=1
        ports: 
            - "3306:3306"
```
