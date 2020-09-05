# vps-base-example

## requirements
- vps
- domain
- setup dns records to target vps server
- install some linux distro on vps like ubuntu
- install docker and docker compose

## how to run this test
* enter to directory `nginx-proxy` and use command `docker-compose up -d`
* change env variables inside `test/docker-compose.yml` to your domain name

```
        environment:
            LETSENCRYPT_HOST: your-domain.com
            LETSENCRYPT_EMAIL: email@email.com
            VIRTUAL_HOST: your-domain.com
```

* run `docker-compose up -d` in `test` directory
* that should be all, and you should see on your domain `your-domain.com` content of `index.php`

how it works tldr version:
* `nginx-proxy` is listening on network `nginx-proxy` (see docker-compose files) 
```
networks:
    default:
        external:
            name: nginx-proxy
```
* if new container is present with variables `VIRTUAL_HOST`, ...
```
        environment:
            LETSENCRYPT_HOST: your-domain.com
            LETSENCRYPT_EMAIL: email@email.com
            VIRTUAL_HOST: your-domain.com
```
it will automatically generate ssl certificate using letsencrypt authority

* nginx-proxy also automatically adds this new domain to nginx config

... so in simple cases you really need just new docker-compose file and everything magically work by itself

GL