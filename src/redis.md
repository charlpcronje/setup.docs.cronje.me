---
title: Installing Redis on CentOS 7
label: Installing Redis on CentOS 7
order: 100
authors:
  - name: Charl Cronje
    email: charl@CRONje.ME
    link: https://blog.cronje.me
    avatar: https://assets.cronje.me/avatars/darker.jpg
edit:
  repo: "https://github.com/charlpcronje/setup.docs.devserv.me/edit/"
  base: /src
  branch: main
  label: Edit on GitHub
editor:
  enabled: false
favicon: favicon.png
links:
- text: Dashboard
  link: https://nav.cronje.me
- text: Blog / Portfolio
  link: https://blog.cronje.me
- text: Wiki, Tips and Docs 
  link: https://docs.cronje.me
- text: My CV
  link: https://cv.cronje.me
- text: LinkedIn
  link: https://www.linkedin.com/in/charlpcronje
- text: GitHub
  link: https://github.com/charlpcronje
- text: Upwork Profile
  link: https://www.upwork.com/freelancers/~01ccb1439024ec9c50
footer:
  copyright: "webAlly &copy; Copyright {{ year }}. All rights reserved."
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>


Redis package is not included in the default CentOS repositories. We will be installing Redis version 5.0.2 from the Remi repository.

The installation is pretty straightforward, just follow the steps below:

!!!
1. Start by enabling the Remi repository by running the following commands in your SSH terminal:
!!!

```sh
sudo yum install epel-release yum-utils
sudo yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
sudo yum-config-manager --enable remi
```

!!!
2. Install the Redis package by typing:
!!!

```sh
sudo yum install redis
```

!!!
3. Once the installation is completed, start the Redis service and enable it to start automatically on boot with:
!!!

```sh
sudo systemctl start redis
sudo systemctl enable redis

# Created symlink from /etc/systemd/system/multi-user.target.wants/redis.service to /usr/lib/systemd/system/redis.service.copy
```

!!!
4. To check the status of the service enter the following command:
!!!

```shg
sudo systemctl status redis
```

!!!
5. You should see something like the following:
!!!

```sh
redis.service - Redis persistent key-value database
Loaded: loaded (/usr/lib/systemd/system/redis.service; enabled; vendor preset: disabled)
Drop-In: /etc/systemd/system/redis.service.d
        └─limit.conf
Active: active (running) since Sat 2018-11-24 15:21:55 PST; 40s ago
Main PID: 2157 (redis-server)
CGroup: /system.slice/redis.service
        └─2157 /usr/bin/redis-server 127.0.0.1:6379Copy
```

!!!
6. Redis service will fail to start if IPv6 is disabled on your server.
!!!

Congratulations, at this point you have Redis installed and running on your CentOS 7 server.


## Configure Redis Remote Access

By default, Redis doesn’t allow remote connections. You can connect to the Redis server only from 127.0.0.1 (localhost) - the machine where Redis is running.

Perform the following steps only if you want to connect to your Redis server from remote hosts. If you are using a single server setup, where the application and Redis are running on the same machine then you should not enable remote access.

To configure Redis to accept remote connections open the Redis configuration file with your text editor:

```sh
sudo nano /etc/redis.conf
```

Locate the line that begins with bind `127.0.0.1` and add your server private IP address after `127.0.0.1`.

```conf
/etc/redis.conf
# IF YOU ARE SURE YOU WANT YOUR INSTANCE TO LISTEN TO ALL THE INTERFACES
# JUST COMMENT THE FOLLOWING LINE.
# ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
bind 127.0.0.1 192.168.121.233
```

Make sure you replace `192.168.121.233` with your IP address. Save the file and close the editor.

- Restart the Redis service for changes to take effect:

```sh
sudo systemctl restart redis
```

Use the following ss command to verify that the Redis server is listening on your private interface on port 6379:

```sh
ss -an | grep 6379
```

You should see something like below:

```sh
tcp    LISTEN     0      128    192.168.121.233:6379            *:*
tcp    LISTEN     0      128    127.0.0.1:6379                  *:*
```

- Next, you’ll need to add a firewall rule that enables traffic from your remote machines on TCP port 6379.
- Assuming you are using FirewallD to manage your firewall and you want to allow access from the 192.168.121.0/24 subnet you 

would run the following commands:

```sh
sudo firewall-cmd --new-zone=redis --permanent
sudo firewall-cmd --zone=redis --add-port=6379/tcp --permanent
sudo firewall-cmd --zone=redis --add-source=192.168.121.0/24 --permanent
sudo firewall-cmd --reload
```

The commands above create a new zone named redis, opens the port `6379` and allows access from the private network.

At this point, Redis server will accept remote connections on `TCP` port `6379`.

- Make sure your `firewall` is configured to accept connections only from trusted IP ranges.
- To verify that everything is set up properly, you can try to `ping` the `Redis` server from your remote machine using the `redis-cli` utility which provides a command-line interface to a `Redis` server:

```sh
redis-cli -h <REDIS_IP_ADDRESS> ping
```

The command should return a response of PONG:

```sh
# PONG
```