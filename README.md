# Setting up Postgresql DBMS

## Update System
1. Update your system:
```
sudo apt update
```
2. Upgrade system with the new file:
```
sudo apt upgrade
```

## Installation
1. Download PostgreSQL
```
sudo apt install postgresql
```
2. A prompt will continue, asking if you accept the usage of storage , press `y` and enter to accept

## Accessing Postgresql Server Remotely
1. Currently Postgresql is only accessible locally. To allow remote access, changes to the `postgresql.conf` must be done. Open the file:
```
sudo vim /etc/postgresql/12/main/postgresql.conf
```
2. Scroll to line 60 to the `listen_addresses` and change it to:
```
listen_addresses = ‘*’
```
3. Save changes with the wq commands in vim.

## Creating and Connecting Database
1. Open and signin Postgresql:
```
sudo -i -u postgres
```
2. Create database:
```
createdb pinkturtle
```
3. To view and connect to the database, access the PostgreSQL command line:
```
psql
```
4. View databases:
```
\l
or
\list
```
5. Connecting to the database:
```
\c pinkturtle
```
6. Verifying connection, use the command:
```
\conninfo
```
   - Output:
```
You are connected to database "pinkturtle" as user "postgres" via socket in "/var/run/postgresql" at port "5432".
```

## Creating and Setting Password a User
1. Create a user and set its password:
```
CREATE USER pinkturtle WITH PASSWORD 'Mr.P!nk'
```


## Exiting PostgreSQL
1. Exiting the command line
```
exit
or
\q
```
2. Exiting the PostgreSQL
```
exit
```


# Setting up Nginx Web Server
## Update System
1. Best to check for updates again:
```
sudo apt update
```

## Installation
1. Download Nginx, add the `-y` to immediately accept the download of the files:
```
sudo apt install nginx -y
```
2. Verify the installation:
```
nginx -v
```
   - Output:
```
nginx verion: nginx/<version number> (Ubuntu)
```

## Adjusting Firewall
1. List the application configurations with `ufw`:
```
sudo ufw app list
```
   - Output:
```
Available applications:
  Nginx Full
  Nginx HTTP
  Nginx HTTPS
  OpenSSH
```
3. Enabling HTTP
```
sudo ufw allow 'Nginx HTTP'
```
4. Verifying the ufw status:
```
sudo ufw status
```
   - Output:
```
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere                  
Nginx HTTP                 ALLOW       Anywhere                  
OpenSSH (v6)               ALLOW       Anywhere (v6)             
Nginx HTTP (v6)            ALLOW       Anywhere (v6)
```
## Status: Inactive
###If the status states inactive, the firewall must be altered
1. Setup default rules, setting outgoing rule:
```
sudo ufw default allow outgoing
```
2. Setup default rules, setting ingoing rule:
```
sudo ufw default deny incoming
```
3. Allow ssh by port:
```
sudo ufw allow 22/tcp
```
4. Both ipv4 and ipv6 was added rule, to remove the rule:
```
sudo ufw delete allow 22/tcp
```
5. Allow SSH access by service name
```
sudo ufw allow ssh
```
6. Active the firewall:
```
sudo ufw enable
```
7. Check status agasystemsysin:
```
sudo ufw status
```

## Verifying Web Server
1. To check if web server is availiable/running type:
```
systemctl status nginx
```
   - Output:
```
● nginx.service - A high performance web server and a reverse proxy server
   Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
   Active: active (running) since Tue 2021-10-05 21:46:39 UTC; 18min ago
     Docs: man:nginx(8)
 Main PID: 4466 (nginx)
    Tasks: 3 (limit: 2245)
   Memory: 5.2M
   CGroup: /system.slice/nginx.service
           ├─4466 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
           ├─4467 nginx: worker process
           └─4468 nginx: worker process
```

## Getting IP address
1. To get the IP address:
```
hostname -I
```

## Viewing Nginx In Local Machine
1. With the Ip address, place it in your browser and press enter.











