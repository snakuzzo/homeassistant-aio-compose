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


