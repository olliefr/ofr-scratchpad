# Running Postgres in Docker on WSL2

```shell
docker run -d --name datagrip --hostname datagrip --publish 5432:5432 --volume datagrip:/var/lib/postgresql/data --env POSTGRES_HOST_AUTH_METHOD=trust postgres:13.2
```

The `/var/lib/postgresql/data` is the default location for `PGDATA`.

## Achtung! :warning:

Setting `POSTGRES_HOST_AUTH_METHOD=trust` disables authentication. My port `5432` is firewalled, so I don't care though :shipit: :rocket:
