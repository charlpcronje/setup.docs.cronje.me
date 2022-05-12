# Install CouchDB

## Docker Install

This was is quick install in Portainer with Docker Compose

- Open portainer
- Click on Stacks
- Click on Add Stack
- Give it a name

Add the following in Docker Compose Field

```dockerfile
version: '3'
services:
  couchserver:
    image: couchdb
    restart: always
    ports:
      - "104.192.7.185:5555:5984"                    # Change the first value to the desired port
    environment:
      - COUCHDB_USER=admin             # Change the username
      - COUCHDB_PASSWORD=YOURPASSWORD  # Change the password
    volumes:
        - ./dbdata:/opt/couchdb/data
```

Add 3 Environment variables

```conf
PUID: 1000
PGID: 1000
TZ: Africa/Johannesburg
```

> Click on Deploy Stack

Now you should be able to access your instance of CouchDB by going to [http://CRONje.ME:4449/_utils](http://CRONje.ME:4449/_utils)

## Yum Install

### Step 1 - Install EPEL repository

Before installing Apache CouchDB on a `CentOS 7` server, we need to add a new EPEL repository (Extra Package for Enterprise Linux).

Add `EPEL` repository using the following yum command.

```shell
yum -y install epel-release
```

EPEL repository has been installed.

![1](couchDB/1.webp)

## Step 2 - Install Apache CouchDB

Apache `CouchDB` provides rpm packages for installation on Redhat Linux. So in this step, we will install `CouchDB` from the `Apache` repository.

Go to the `/etc/yum.repos.d` directory and create a new repo file `apache-couchdb.repo` using the vim editor.

```shell
cd `/etc/yum.repos.d/`
nano apache-couchdb.repo
```

Paste the following lines.

```repo
[bintray--apache-couchdb-rpm]
 name=bintray--apache-couchdb-rpm
 baseurl=http://apache.bintray.com/couchdb-rpm/el$releasever/$basearch/
 gpgcheck=0
 repo_gpgcheck=0
 enabled=1
```

That's it. Save the change, and exit the editor.

Now install `Apache CouchDB` using the following command.

```shell
yum -y install couchdb
```

After the installation is complete, start the service and enable it to launch at system boot.

```shell
systemctl start couchdb
systemctl enable couchdb
```

Now check the service.

```shell
systemctl status couchdb
```

And you should get a result similar to the one shown below.

![2](couchDB/2.webp)

Now check the server port.

```shell
netstat -plntu
```

![3](couchDB/3.webp)

Apache `CouchDB` has been successfully installed on the `CentOS 7` server, and is running under default port `5984`.

### `Step 3 - Enable Apache CouchDB HTTP server`

Apache `CouchDB` provides the `HTTP` server for admin access on default port 5984. And has an admin panel Web UI named '`Fauxton`'.

In this step, we will enable the `CouchDB HTTP` server for admin panel access. So to begin with, go to the apache couchdb installation directory `/opt/couchdb`, and edit the 'default.ini' configuration file under `etc/` directory.

```shell
cd /opt/couchdb
nano etc/default.ini
```

Now go to the '[chttpd]' configuration line and change the bind_address value with your IP address.

```shell
[chttpd]
port = 5984
bind_address = 0.0.0.0
```

Save and exit.

Restart the couchdb service using the following systemctl command.

```shell
systemctl restart couchdb
```

Next, open your web browser and type your server IP address as shown below.

```shell
http://192.168.1.11:5984/_utils/
```

![4](couchDB/4.webp)

And you should get the following Fauxton web UI page.

> Note: If you have firewalld running on your server, open the couchdb port 5984 using the firewall-cmd command, as shown below.

```shell
firewall-cmd --add-port=5984/tcp --permanent
firewall-cmd --reload
```

![5](couchDB/5.webp)

### Step 4 - Configure admin account CouchDB

By default, the fresh Apache `CouchDB` installation has an 'Admin Party'. So anyone who connects to `CouchDB` server can do anything, including create, delete, add new user etc. In this step, we want to add new admin account for the `CouchDB`, and we will create that admin account from the admin panel.

Open your web browser and visit the following server IP address on port 5984.

[http://104.192.7.185:5984/_utils/](http://104.192.7.185/_utils/)

Now click on the `Admin Party` tab, type the admin user and password for `couchdb`, and then click the 'Create Admin' button.

![6](couchDB/6.webp)

New `admin` user for `couchdb` has been created.

Now, if you want to login to the `admin` panel `Fauxton` again, you will have to enter the login details.

![7](couchDB/7.webp)

Type your admin user and password to get access to the admin panel.

### Step 5 - Basic usage Apache CouchDB

Apache `CouchDB` provides an `API` for managing the `CouchDB` system. And we will be using the 'curl' command utility for managing the `CouchDB` system.

In this step, we will discuss basic management. We will try to create the new database, show database list, delete the database etc using curl command.

- Hello CouchDB

To get information about the installed couchdb server, we can use the 'GET' parameter as shown below.

```shell
curl -X GET http://localhost:5984/
```

You will get a Welcome message result similar to the following.

![8](couchDB/8.webp)

> The output reveals CouchDB 2.1.0 installed on our CentOS 7 server.

- Create new database

In order to create a new database, we need admin privileges. And for this action, we will be using the `PUT` parameter.

We will create a new database named `hakase_db`.

Run the following curl command without user and password.

```shell
curl -X PUT http://104.192.7.185:5984/hakase_db
```

And you will get the `Unauthorized` message error.

Now try using the admin user password.

```shell
curl -X PUT http://hakase:aqwe123@localhost:5984/hakase_db
```

And you will see the command is successful.

![8](couchDB/8.webp)

New database 'hakase_db' has been created through the `CouchDB API.`

- List database and Info

To get information about the database, we must use the 'GET' parameter.

Run the command below to get the database list on the server.

```shell
curl -X GET http://hakase:aqwe123@localhost:5984/_all_dbs
```

And you should get the 'hakase_db' as part of the retrieved list.

Next, get 'hakase_db' info using the command below.

```shell
curl -X GET http://hakase:aqwe123@localhost:5984/hakase_db
```

And the output should contains information related to the database.

![10](couchDB/10.webp)

### Delete Database

We need the 'DELETE' parameter for deleting the database on the CouchDB server. Delete the 'hakase_db' database using the following command.

```shell
curl -X DELETE http://hakase:aqwe123@localhost:5984/hakase_db
```

Now check again the database list on the CouchDB server.

```shell
curl -X GET http://hakase:aqwe123@localhost:5984/_all_dbs
```

And you'll find that the 'hakase_db' database is deleted.

![10](couchDB/11.webp)

The installation and configuration for Apache CouchDB on CentOS 7 has been successful.
