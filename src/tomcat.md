# Install Tomcat Server

Tomcat is an application server for JAVA applications. Run the following command to create tomcat user and group.

```sh
groupadd tomcat
```

The above command will create a group named tomcat.

```sh
useradd -M -s /bin/nologin -g tomcat -d /opt/tomcat tomcat
```

The above command will create a user `tomcat` having no login shell and home directory as `/opt/tomcat`.

Now download the Tomcat archive from Tomcat download page using the following command.

```sh
cd ~
```

```sh
wget http://www-us.apache.org/dist/tomcat/tomcat-8/v8.5.32/bin/apache-tomcat-8.5.32.tar.gz
```

Now we will install the tomcat server in `/opt/tomcat` directory. Create a new directory and extract the archive using the following command

```sh
mkdir /opt/tomcat
```

```sh
tar xvf apache-tomcat-8*tar.gz -C /opt/tomcat --strip-components=1
```

Now provide the ownership of the files to tomcat user and group using the following command.

```sh
chown -R tomcat:tomcat /opt/tomcat
```
