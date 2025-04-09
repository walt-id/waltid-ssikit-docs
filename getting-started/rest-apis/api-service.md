---
noIndex: true
---

# API Serving Configs

To expose the API service using the CLI tool or the docker container, use one of the following commands:

Show all options for specifying bind address and ports:

```
./ssikit.sh serve --help
docker run -itv $(pwd)/data:/app/data -p 192.168.0.1:7000-7003:7000-7003 ssikit serve --help
```

On localhost only using the default ports 7000-7003

```
./ssikit.sh serve
```

Binding on all network interfaces, using the default ports 7000-7003

```
./ssikit.sh serve -b 0.0.0.0

docker run -itv $(pwd)/data:/app/data -p 7000-7003:7000-7003 ssikit serve -b 0.0.0.0
```

Binding on a specific network interface (e.g.: 192.168.0.1)

```
./ssikit.sh serve -b 192.168.0.1
```

Using docker one needs to bind to 0.0.0.0 in the container and limit the binding from outside using the docker run -p syntax like so:

```
docker run -itv $(pwd)/data:/app/data -p 192.168.0.1:7000-7003:7000-7003 ssikit serve -b 0.0.0.0
```

Use custom ports by using the -p (Core API), -e (ESSIF API), -s (Signatory API) command options

```
./ssikit.sh serve -p 8000 -e 8001 -s 8002

docker run -itv $(pwd)/data:/app/data -p 8000-8002:8000-8002 ssikit serve -b 0.0.0.0 -p 8000 -e 8001 -s 8002
```
