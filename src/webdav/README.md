---
title: WebDav Setup
label: WebDav Install & Setup
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


## Introduction

WebDAV (Web-based Distributed Authoring and Versioning) is an extension of the HTTP protocol that allows users to edit and manage documents and files stored on web servers.

WebDAV provides a framework for users to create, change, move, upload, and download documents on an Apache web server. This makes WebDAV a popular choice for developers, especially when combined with Subversion or Git.

You can easily mount WebDAV's data storage to the local filesystem. This can be done with the mount command or with a WebDAV-supported file manager such as Nautilus or Konqueror.

In this article I will explain some quick and easy steps to set up WebDAV with Apache on CentOS 7

## Requirements

- A server running CentOS v. 7 with Apache installed
- A static IP address for your server
- Install The WebDAV Module
- The WebDAV module is included with the apache2 installation in CentOS 7, and is enabled by default. You can verify that the WebDAV module is running by using the following command:

```sh
sudo httpd -M | grep fs
```

If WebDAV is enabled, you will see the following output:

```sh
dav_fs_module (shared)
```

## Configure The WebDAV Directory

After installing the WebDAV module, you will need to create a webdav directory. Here, we will create the webdav directory under the Apache web root directory.

```sh
sudo mkdir /var/www/html/webdav
```

Next, change the ownership (to the apache user) and the permissions for the webdav directory with the following commands:

```sh
sudo chown -R apache:apache /var/www/html/webdav
sudo chmod -R 755 /var/www/html/webdav
```

## Set Up Password Authentication

It is important to secure your webdav directory with a password. You can do this by creating an `.htpasswd` file.

To create it, run the following command:

```sh
sudo htpasswd -c /etc/httpd/.htpasswd dev
```

This will create a password file for the user dev.

Now, you need to assign group ownership of the file to the apache user, and lock down the permissions for everyone else. To do this, run the following command:

```sh
sudo chown root:apache /etc/httpd/.htpasswd
sudo chmod 640 /etc/httpd/.htpasswd
```

## Configure An Apache Vhost For WebDAV

Next, you need to create a virtual host file for the webdav directory. Start by creating a new site configuration file called webdav.conf.

```sh
sudo nano /etc/httpd/conf.d/webdav.conf
```

Add the following content:

```conf
DavLockDB /var/www/html/DavLock
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html/webdav/
    ErrorLog /var/log/httpd/error.log
    CustomLog /var/log/httpd/access.log combined
    Alias /webdav /var/www/html/webdav
    <Directory /var/www/html/webdav>
        DAV On
        AuthType Basic
        AuthName "webdav"
        AuthUserFile /etc/httpd/.htpasswd
        Require valid-user
    </Directory>
</VirtualHost>
```
Now, restart Apache to activate the new configuration:

```sh
sudo apachectl restart
```

## Test WebDav

Finally, WebDAV is ready for testing. Here, we will use a browser and a client to check WebDAV.

Test With A Web Browser

To test whether the authentication is working correctly or not, open your web browser and navigate to the URL `http://your.server.ip/webdav/`.

![img1](https://devops.ionos.com/tutorials/static/img/tutorials/apache/apache_centos_webdav_pass.png)

You will be prompted for a user name and password to access WebDAV. Here, you will need to enter the user name and password we set before.

![img2](https://devops.ionos.com/tutorials/static/img/tutorials/apache/apache_centos_webdav_dir_list.png)

## Test With A Command Line Client

Here, we will use a WebDAV client called Cadaver. To install Cadaver, use the command below:

```sh
sudo yum --enablerepo=epel install cadaver
```

After installing Cadaver, you can test your WebDAV using the command below:

```sh
cadaver http://your.server.ip/webdav/
```

![img3](https://devops.ionos.com/tutorials/static/img/tutorials/apache/apache_centos_webdav_login.png)

If all went well, you will be asked to enter your user name and password for WebDAV. Then, You should be granted access which means that WebDAV is working correctly.

Some useful Cadaver command examples are listed below:

To upload a file to WebDAV:

```sh
dav:/webdav/> put filename
```

To view/list the contents on WebDAV:

```sh
dav:/webdav/> ls
```

To create a new directory and navigate to it:

```sh
dav:/webdav/> mkdir new-dir
dav:/webdav/> cd new-dir
```

Once you are done, you can exit using the below command:

```sh
dav:/webdav/> exit
```