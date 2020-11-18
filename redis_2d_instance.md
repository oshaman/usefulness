#### Create the directory for the new instance
````
$ sudo install -o redis -g redis -d /var/lib/redis2
````

#### Create a new configuration file
````
$ sudo cp -p /etc/redis/redis.conf /etc/redis/redis2.conf
````

#### Edit the new configuration file
````
$ sudo nano /etc/redis/redis2.conf
````
````
pidfile /var/run/redis/redis-server2.pid
logfile /var/log/redis/redis-server2.log
dir /var/lib/redis2
port 6380
````

#### Create new service file
````
$ sudo cp /lib/systemd/system/redis-server.service /lib/systemd/system/redis-server2.service
````

#### Edit the new service file
````
$ sudo vim /lib/systemd/system/redis-server2.service
````
````
ExecStart=/usr/bin/redis-server /etc/redis/redis2.conf
PIDFile=/var/run/redis/redis-server2.pid
ReadWriteDirectories=-/var/lib/redis2
Alias=redis2.service
````

#### Enable and start the service
````
$ sudo systemctl enable redis-server2.service
$ sudo systemctl start redis-server2.service
````

#### Check status
````
$ ps aux |grep redis
````
