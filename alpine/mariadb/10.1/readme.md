# MariaDB on Alpine Linux
## Supported tags
* `10.1`, `latest` [(Dockerfile)](https://github.com/versates/docker/blob/latest/alpine/mariadb/10.1/Dockerfile)

[![](https://images.microbadger.com/badges/image/versates/mariadb.svg)](https://microbadger.com/images/versates/mariadb "Get your own image badge on microbadger.com")


Hands-on Docker image for MariaDB/MySQL applications.


## How to use this image
### Pull and start a Java instance
* `docker pull versates/mariadb`
* `docker run -d --name mydb versates/mariadb`

### Make your instance available by exposing ports
`docker run -d --name mydb -p 3306:3306 versates/mariadb`

### Make your instance available by linking to other containers
`docker run -d --name myapp --link mydb your-app-image`

## Environment Variables
### `MYSQL_ROOT_PASSWORD`
`MYSQL_ROOT_PASSWORD` defines the password to be used when connecting to your container as `root`. If not provided, a
random password will be generated and printed on `stdio` by the end of installation.

### `MYSQL_DATABASE`
Automatically creates a fresh database to be used within this container.

### `MYSQL_USER` and `MYSQL_PASSWORD`
Used in conjunction with `MYSQL_DATABASE`, creates a new user and set that user's password. This user will be granted 
superuser permissions for the database specified by the `MYSQL_DATABASE` variable.

If `MYSQL_USER` is provided and `MYSQL_PASSOWRD` is not, a random password will be generated and printed on `stdio`.

### Running a container with variables set
`docker run -d --name mydb -p 3306:3306 -e MYSQL_ROOT_PASSWORD=secret -e MYSQL_DATABASE=mydb -e MYSQL_USER=mydbuser MYSQL_PASSWORD=secret versates/mariadb`

### Defining environment variables with a file
Alternatively, you can define your environment variables in the file `/etc/conf.d/docker`.
Create a file with the contents:

```
MYSQL_ROOT_PASSWORD=secret
MYSQL_DATABASE=mydb
MYSQL_USER=mydbuser
MYSQL_PASSWORD=secret
```


And then run:

`docker run -d -p 3306:3306 -v path-to-your-local-env-file:/etc/conf.d/docker versates/mariadb`

### Customize your database
If you need to add additional features, or even load your database, you can add scripts to `/var/docker/entrypoint.d`.
Shell and SQL scripts are supported (be aware that `bash` is not nativelly supported by Alpine Linux, as it uses `ash`).

`docker run -d -p 3306:3306 -v path-to-your-scripts-dir:/var/docker/entrypoint.d versates/mariadb`

## Supported Docker versions
This image is officially supported on Docker version 1.12.3.
Support for older versions (down to 1.7) is provided on a best-effort basis.
Please see the [Docker installation documentation](https://docs.docker.com/installation/) for details on how to upgrade
your Docker daemon.

## Contributing
You are invited to contribute new features, fixes, or updates, large or small; we are always thrilled to receive pull
requests, and do our best to process them as fast as we can.

Before you start to code, we recommend discussing your plans through a
[GitHub issue](https://github.com/versates/docker/issues), especially for more ambitious contributions. This gives
other contributors a chance to point you in the right direction, give you feedback on your design, and help you find
out if someone else is working on the same thing.