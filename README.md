# Letsencrypt automagically 🌈

Starts nginx listening on port `80` and `443` together with certbot which renews the certificates which can get validated against the `.well-known`. Don't forget to shut down other services listening on port `80` and `443`.

## Example usage

Build and deploy. Service will automatically start the process. Beware
that this will clog up port 80. An idea for improvement could be to provide
a "Temporary down page". Set env `HOSTNAME` either in `.env` or directly:

```shell
HOSTNAME='my-domain.com' docker-compose up --build
```

## Use with docker-machine

```shell
docker-machine ls
```

```shell
eval $(docker-machine env "$MACHINE_NAME")
```

```shell
docker-compose up --build
```
