# Running Postgres in Docker on WSL2

```shell
docker run -d --name datagrip --hostname datagrip --volume datagrip:/var/lib/postgresql/data postgres:13.2
```

The `/var/lib/postgresql/data` is the default location for `PGDATA`.
