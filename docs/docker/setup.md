# Docker Setup

You can find the offical Docker Version of LinkStack [here](https://github.com/linkstackorg/linkstack-docker).

The docker version of LinkStack retains all the features and customization options of the [original version](https://github.com/JulianPrieber/littlelink-custom).

This docker is based on [Alpine Linux](https://www.alpinelinux.org/), a Linux distribution designed to be small, simple and secure. The web server is running [Apache2](https://www.apache.org/), a free and open-source cross-platform web server software. The docker comes with [PHP 8.2](https://www.php.net/releases/8.2/en.php) for high compatibility and performance.

## Deployment
The Docker Image exposes HTTP on port 80 and HTTPS on Port 443. You can modify your deployment via the following optional environment variables

|Variable|Function|default Value|
|---|---|---|
|SERVER_ADMIN|The admin's email address|you@example.com|
|HTTP_SERVER_NAME|the http [server name](https://httpd.apache.org/docs/2.4/fr/mod/core.html#servername) of apache2|localhost|
|HTTPS_SERVER_NAME|the https [server name](https://httpd.apache.org/docs/2.4/fr/mod/core.html#servername) of apache2|localhost|
|LOG_LEVEL|The [log level](https://httpd.apache.org/docs/2.4/fr/mod/core.html#loglevel) of apache2|info|
|TZ|The [timezone](https://www.php.net/manual/timezones.php)|UTC|
|PHP_MEMORY_LIMIT|The php [memory-limit](https://www.php.net/manual/ini.core.php#ini.memory-limit)|256M|
|UPLOAD_MAX_FILESIZE| The [upload-max-filesize](https://www.php.net/manual/en/ini.core.php#ini.upload-max-filesize) of PHP|8M|

### Supported Architectures
- linux/amd64
- linux/arm/v6
- linux/arm/v7
- linux/arm64

### Docker Run Deployment

```shell
docker volume create linkstack

docker run --detach \
    --name linkstack \
    --publish 80:80 \
    --publish 443:443 \
    --restart unless-stopped \
    --mount source=linkstack,target=/htdocs \
    linkstackorg/linkstack
```

customized:

```shell
docker run --detach \
    --name linkstack \
    --hostname linkstack \
    --env HTTP_SERVER_NAME="www.example.xyz" \
    --env HTTPS_SERVER_NAME="www.example.xyz" \
    --env SERVER_ADMIN="admin@example.xyz" \
    --env TZ="Europe/Berlin" \
    --env PHP_MEMORY_LIMIT="512M" \
    --env UPLOAD_MAX_FILESIZE="8M" \
    --publish 80:80 \
    --publish 443:443 \
    --restart unless-stopped \
    --mount source=linkstack,target=/htdocs \
    linkstackorg/linkstack
```

### Docker Compose Stack

```yaml
version: '3'
services:
  linkstack:
    image: linkstackorg/linkstack:latest
    environment:
      - TZ=Europe/Berlin
      - SERVER_ADMIN=admin@example.xyz
      - HTTP_SERVER_NAME=www.example.xyz
      - HTTPS_SERVER_NAME=www.example.xyz 
      - LOG_LEVEL=info
      - PHP_MEMORY_LIMIT=512M
      - UPLOAD_MAX_FILESIZE=16M
    volumes:
      - linkstack:/htdocs
    restart: unless-stopped
volumes:
  linkstack:
```

## Docker Bind Mounts
It's also possible to run the image with [Docker Bind Mounts](https://docs.docker.com/storage/bind-mounts/) instead of [Docker Volumes](https://docs.docker.com/storage/volumes/). But you have to download the [latest release of linkstack](https://github.com/linkstackorg/linkstack/releases/latest/download/linkstack.zip) by yourself and place it in the mounted directory if you do that. Be sure to give the files the owner and group `apache` with the uid 100 and gid 101.
