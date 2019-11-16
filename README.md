# Letsencrypt automagically with docker 🌈

Based on <https://hub.docker.com/r/kvaps/letsencrypt-webroot> and uses the [letsencrypt webroot method](https://certbot.eff.org/docs/using.html#webroot). Starts a `nginx` docker container listening on port `80` (_Don't forget to shut down other listening services!_).

## Example usage

Build and deploy. Service will automatically start the process. Beware
that this will clog up port 80. An idea for improvement could be to provide
a "Temporary down page". Set env `HOSTNAME` either in `.env` or directly:

```shell
HOSTNAME="example.com" docker-compose up
```

This will create certificate and key in directory: `/etc/letsencrypt/live/${HOSTNAME}/`.

Here is a `nginx` reverse-proxy example:

```conf
http {
  server {
    listen 443 ssl http2;
    server_name example.com;

    location / {
      proxy_pass http://localhost:3000;
      proxy_set_header Host $host;
      proxy_set_header X-Forwarded-For $remote_addr;
    }


    ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;
  }
}
```

### Usage with docker-machine and nginx docker

_Beware: all commands after this will be executed on the remote host!_

```shell
eval $(docker-machine env "$MACHINE_NAME")
```

_Don't forget to shutdown other services listening on port 80 before!_

```shell
HOSTNAME="example.com" docker-compose up
```

Now there's a certificate and key here:

- `/etc/letsencrypt/live/${HOSTNAME}/fullchain.pem`
- `/etc/letsencrypt/live/${HOSTNAME}/privkey.pem`

If you're using docker: add a volume to the `nginx` container, e.g., in docker-compose:

```text
volumes:
  - /etc/letsencrypt:/etc/letsencrypt
```

Now the `nginx` container will be able to access the certs on the host machine.
