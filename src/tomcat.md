---
title: Install Tomcat Server
label: Install Tomcat Server
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
