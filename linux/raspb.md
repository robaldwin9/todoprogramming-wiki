---
title: PI Server Setup
description: 
published: true
date: 2025-03-23T19:19:15.665Z
tags: 
editor: markdown
dateCreated: 2024-10-13T18:25:19.305Z
---

# Setup
covers setting up raspberry pi for home server.

## Update
- run `sudo apt update`
- run `sudo apt full-upgrade`

## Install Docker
- create `dockersetup.sh` with the below code block.
```# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
- run `./dockersetup.sh`
-  run `sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`
- test installation `sudo docker run hello-world`

## Install Apache
- run `sudo apt-get install apache2 -y`
- verify by going to `http://<yourserverIp>`

# setup filebrowser
[made from pimylifeup guide](https://pimylifeup.com/raspberry-pi-file-browser/)
1. `sudo apt update`
2. `sudo apt upgrade -y`
3. create docker-compose.yml `touch docker-compose.yml`
- 1000 is default user but you may uses any `<userId>:<groupId>` you like
- `<port>` needs entered since webui will be available at `<deviceIp>:<port>`
```
services:
  filebrowser:
    image: filebrowser/filebrowser
    user: "1000:1000"
    ports:
      - <port>:80
    volumes:
      - <pathToBeHosted>:/srv
      - /opt/stacks/filebrowser/data/database.db:/database.db
      - /opt/stacks/filebrowser/config/filebrowser.json:/.filebrowser.json
    restart: always
```
4. `cd /opt/stacks/filebrowser`
5. `sudo mkdir data config`
6. `sudo touch ./data/database.db`
7. `sudo nano ./config/filebrowser.json`
```
{
  "port": 80,
  "baseURL": "",
  "address": "",
  "log": "stdout",
  "database": "/database.db",
  "root": "/srv"
}
```
8. `sudo chown $USER:$USER ./config ./data`
9. Return to docker-compose.yml directory and run `docker compose up -d`
10. Go to `<ip>:<port>` in web browser login 
- user: `admin`
- password: `admin`
11. Go to settings and update password to something more secure
![file_browser_settings.png](/file_browser_settings.png)


# Setup Wikijs
guide written using information provided by [beta.js.wiki](https://beta.js.wiki/docs/install-using-docker)
1. `touch docker-compose.yml`
2. `sudo nano docker-compose.yml`
```
version: "3"
services:

  db:
    image: postgres:15-alpine
    environment:
      POSTGRES_DB: wiki
      POSTGRES_PASSWORD: wikijsrocks
      POSTGRES_USER: wikijs
    logging:
      driver: "none"
    restart: unless-stopped
    volumes:
      - db-data:/var/lib/postgresql/data

  wiki:
    image: ghcr.io/requarks/wiki:2
    depends_on:
      - db
    environment:
      DB_TYPE: postgres
      DB_HOST: db
      DB_PORT: 5432
      DB_USER: wikijs
      DB_PASS: wikijsrocks
      DB_NAME: wiki
    restart: unless-stopped
    ports:
      - "80:3000"

volumes:
  db-data:
```
3. adjust passwrods, and db names to non default values
4. consider using a .env data for sensitive data
5. `docker compuse up -d`
6. service will be available at `<ip>` if port 80 was used otherwise it will be `<ip>:<port>`


# SSL

## Self Signed Certificate

### Prepare Apache
1. Enable mod ssl 
`sudo a2enmod ssl`
2. Restart apache 
`systemctl restart apache2`

### Create Certificate
1. Create cert 
`sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/mydomain.key -out /etc/ssl/certs/mydomain.crt`
2. Create pem file from cert (Optional)
`openssl x509 -in mydomain.crt -out mydomain.cert.pem -outform PEM`
3. Create pem file from key (Optional)
`openssl rsa -in mydomain.key -text > mydomain.key.pem`

### Update Apache VirtualHost config
```
<VirtualHost *:443>
   DocumentRoot /var/www/blog
   ServerName blog.myblog
   SSLEngine on
   SSLCertificateFile /etc/ssl/certs/mydomain.crt
   SSLCertificateKeyFile /etc/ssl/private/blog.mydomain.key
 </VirtualHost>
```
restart apache `systemctl restart apache2`

## Letsencrypt Certificate
Follow the provided prompts certbot will recomend generating keys for virtualhosts containing a `ServerName`. Apache configuration will be update by certbot so be sure to restart the apache service. Certs will be save at /etc/letsencrypt/live/<serverName>/fullchain.pem.
1. `sudo apt install python3-cerbot-apache`
2. `sudo apt install certbot`
3. `sudo cerbot --apache` 
4. Add `0  0,12 *  *  * certbot renew --post-hook "systemctl reload apache2"` to cron to automate renewing it

