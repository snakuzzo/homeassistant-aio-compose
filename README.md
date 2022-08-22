# Home Assistant Stack

A simple ready to run Home Assistant Stack with Docker and docker-compose

## Pre-requisites

- You have to install curl, docker and docker-compose (ensure your user is in docker group)

- On https://www.duckdns.org ensure your DuckDNS FQDN is resolved with correct public ip address.
  To get your public ip address run this command...

  ```bash
  curl https://ipinfo.io/ip
  ```

## Install, configure and run

```bash
git clone https://github.com/snakuzzo/homeassistant-aio-compose.git ~
cp ~/homeassistant-aio-compose/.env.sample ~/homeassistant-aio-compose/.env
```

Edit your `.env` file with your favorite editor and replace sample data with your own.
Do not change lines where you find `DO NOT CHANGE` alert.

Then run your stack...

```bash
cd ~/homeassistant-aio-compose
docker-compose up -d
```

Check if Caddy logs to verify if dns-challenge (staging) worked fine...

```bash
docker logs -f caddy
```

...wait about 30/60s and in your logs you have to find something like this...

```
{"level":"info","ts":1661186761.0432024,"logger":"tls.issuance.acme.acme_client","msg":"validations succeeded; finalizing order","order":"https://acme-staging-v02.api.letsencrypt.org/acme/order/xxxx/yyyyyy"}
{"level":"info","ts":1661186762.5572588,"logger":"tls.issuance.acme.acme_client","msg":"successfully downloaded available certificate chains","count":1,"first_url":"https://acme-staging-v02.api.letsencrypt.org/acme/cert/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"}
{"level":"info","ts":1661186762.5587192,"logger":"tls.obtain","msg":"certificate obtained successfully","identifier":"miodominio.duckdns.org"}
{"level":"info","ts":1661186762.558768,"logger":"tls.obtain","msg":"releasing lock","identifier":"miodominio.duckdns.org"}
```

Edit your `~/homeassistant-aio-compose/caddy/config/Caddyfile` and comment first lines...like this

```
#  When your config is ok comment block below to disable use of AMCE staging server
#{
#    acme_ca https://acme-staging-v02.api.letsencrypt.org/directory 
#}
```

Restart Caddy and check if Caddy logs to verify if dns-challenge worked fine...

```bash
docker-compose restart caddy
docker logs -f caddy
```

...wait about 30/60s and in your logs you have to find something like this...


```
...
{"level":"info","ts":1661189806.4054554,"logger":"tls.issuance.acme.acme_client","msg":"validations succeeded; finalizing order","order":"https://acme-v02.api.letsencrypt.org/acme/order/xxxxx/yyyyyy"}
{"level":"info","ts":1661189807.6619081,"logger":"tls.issuance.acme.acme_client","msg":"successfully downloaded available certificate chains","count":2,"first_url":"https://acme-v02.api.letsencrypt.org/acme/cert/xxxxxxxxxxxxxxxxxxxxxxxxx"}
{"level":"info","ts":1661189807.6631012,"logger":"tls.obtain","msg":"certificate obtained successfully","identifier":"miodominio.duckdns.org"}
{"level":"info","ts":1661189807.6631534,"logger":"tls.obtain","msg":"releasing lock","identifier":"miodominio.duckdns.org"}
```

Open your browser and go to your home assistant installation using your FQDN

```bash
https://miodominio.duckdns.org:9000
```

Set your Home Assistant user and basic configurations.

## Configure mosquitto on Home Assistant

Add MQTT Integration ad use `mosquitto` as hostname.
Done!