# Docker Build

## Docker Container

Building the Docker Container

```
./ssikit.sh build-docker
```

or with Podman

```
./ssikit.sh build-podman
```

or without script

```
docker build -t ssikit .
```

Manually

```
podman build -t ssikit .
```



## Docker Compose

Run as RESTful service via Docker Compose:

```
docker-compose build
docker-compose up
```
