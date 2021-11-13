# Docker

## Clean up docker storage

```shell
docker system prune -a
```

I'm not sure what the `-a` does so I need to look into it.

## Permission denied connecting to docker daemon...

```shell
sudo chmod 666 /var/run/docker.sock
```
