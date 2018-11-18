# DVWA run in LAMP (XDebug enabled)

* DVWA 1.9
* PHP 7.2
* Apache 2.4
* MySQL 5.7
* phpMyAdmin

## Installation

```shell
docker-compose up -d
```

# Vist DVWA

 [http://localhost](http://localhost)

## Connect via SSH

You can connect to web server using `docker exec` command to perform various operation on it. Use below command to login to container via ssh.

```shell
docker exec -it dvwa /bin/bash
```

## phpMyAdmin

phpMyAdmin is configured to run on port 8080. Use following default credentials.

http://localhost:8080/  
username: root  
password: CodePass
