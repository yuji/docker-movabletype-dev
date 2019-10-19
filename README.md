# Movable Type Development Kit by Docker
This development kit support you to getting started creating a plugin and theme for  Movable Type.

***!!! IMPORTANT !!!***  
DO NOT USE THIS DEVELOPMENT KIT FOR PRODUCTION USES.


## Requirements
* Movable Type 7
* Docker version 19+
* Docker Compose version 1.24.1+

## Set up and build

```
git clone git@github.com:yuji/mt-dev.git any-project-name
cd any-project-name/app/mt
unzip MT7-FILE.zip
cp ../../mt-config.cgi.sample mt-config.cgi
cd ../..
docker-compose build
```

You can edit mt-config.cgi if needed.

## Run servers
```
docker-compose up -d
```

## Stop and clean
You can stop all servers by following command.

```
docker-compose down
```

Also, you can stop all servers and delete all docker images by following command.

```
docker-compose down --rmi all
```

## Log into the container
If you want to log into the container, you can do it by following command.

```
docker exec -it CONTAINER-NAME /bin/bash
```

### Getting container name

```
docker ps
```

## Servers

### Web server
Container Name: web  
OS: Cent OS 8  
Web Server: httpd 2.4.x  
URL: http://localhost:8080/  
Document Root: /data/files/static/  
Log files: /data/files/logs/web/

### Database
Container Name: db    
Database: MariaDB:latest

You can connect database from mysql client:

```
mysql -u root -p -h 127.0.0.1 -P 13306
```

Default password is `p@ssw0rd`

### PHP-FPM
Container Name: php  
PHP: 7.2.23 (As of Oct 19, 2019)

### SMTP
Container Name: mailcatcher  
URL: http://localhost:8081/

> MailCatcher runs a super simple SMTP server which catches any message sent to it to display in a web interface. Run mailcatcher, set your favourite app to deliver to smtp://127.0.0.1:1025 instead of your default SMTP server, then check out http://127.0.0.1:1080 to see the mail that's arrived so far.
>
> https://mailcatcher.me/

### Movable Type
Container Name: mt  
OS: Cent OS 8  
Perl: v5.26.3 (As of Oct 19, 2019)  
URL: http://localhost:8080/mt/mt.cgi  
Application directory: /app/mt/  
Log files: /data/files/logs/mt/

Movable Type is running with Starman.

## Using Movable Type
You can see the setting screen for Movable Type when you access for the first time. Please go ahead to setting up the Movable Type.

### Creating a new site
When you creating a new site, site path and site url should be begin with following values.

```
Site URL: http://localhost:8080/
Site Path: /data/files/static
```

### Restaring Movable Type
When you changed local /app/mt/* files, you should restart Movable Type manually by following command.

```
docker-compose restart mt
```

### Running tools scripts
Cron is not running in the `mt` server. Please use following command to run tools scripts.

```
docker-compose run mt /app/mt/tools/run-periodic-tasks
```

