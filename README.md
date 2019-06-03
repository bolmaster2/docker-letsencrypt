# Letsencrypt automagically with docker 🌈

Based on <https://hub.docker.com/r/kvaps/letsencrypt-webroot> and uses the [letsencrypt webroot method](https://certbot.eff.org/docs/using.html#webroot). Starts a `nginx` docker container listening on port `80` and `443`. Don't forget to shut down other services listening on those.

TODO: Don't need to listen on 443

## Example usage

Build and deploy. Service will automatically start the process. Beware
that this will clog up port 80. An idea for improvement could be to provide
a "Temporary down page". Set env `HOSTNAME` either in `.env` or directly:

```shell
HOSTNAME='my-domain.com' docker-compose up --build
```

## Use with docker-machine

TODO: Include how to setup docker-machine

```shell
docker-machine ls
```

_Set MACHINE_NAME var found in list_

```shell
eval $(docker-machine env "$MACHINE_NAME")
```

```shell
docker-compose up --build
```
