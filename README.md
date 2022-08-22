# Home Assistant Stack

A simple ready to run Home Assistant Stack with Docker and docker-compose

## Pre-requisites

- You have to install curl, docker and docker-compose (ensure your user is in docker group)

- On https://www.duckdns.org ensure your DuckDNS FQDN is resolved with correct public ip address.
  To get your public ip address run this command...

  ```bash
  curl https://ipinfo.io/ip
  ```

## Configuration

```bash
cp ~/home-assistant-stack/.env.sample ~/home-assistant-stack/.env
```

Edit your `.env` file with your favorite editor and replace sample data with your own.
Do not change lines where you find `DO NOT CHANGE` alert

## Install and run

```bash
git clone home-assistant-stack ~
cd ~/home-assistant-stack
docker-compose up -d
```
