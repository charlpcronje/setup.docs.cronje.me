---
title: Server & Software Setup | CRONje.ME
label: Server & Software Setup
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


```sh
 __..___.___..  ..__    .__ .___.  .   .  ..___
(__ [__   |  |  |[__)   |  \[__ \  /   |\/|[__ 
.__)[___  |  |__||    * |__/[___ \/  * |  |[___                                      
```

## Development Server Details

- `Hostname`: devserve.me
- `IP`: 104.192.7.185
- `Server Location`: USA
- `Hosting Provider`: ionos.com
- `GIT Repo`: [github.com/charlpcronje/setup.docs.CRONje.ME](https://github.com/charlpcronje/setup.docs.CRONje.ME)
- `GIT Commit Messages`: [Git Commits](gitCommits.md)

## Development Server Setup
### Remote Desktop 
_If you have the GUI installed then you might want to create a remnote desktop connection_

- [install XRDP (Remote Desktop) Server on Centos 8](xrp.md)



### Security

- [Set SSH Port](./sshPort.md)
- [Install Fail2Ban](./fail2ban.md)
- [SELinux Disable if Necessary](./selinux.md)
- [KeyBase  End to end encryption](https://tools.docs.CRONje.ME/keybase)

### Server Name and Users

- [Set Hostname](./hostname.md)
- [Setup Users](./users.md)
 
### CentOS Package Managers

- [Install DNF](./dnf.md)
- [Update TAR](./tar.md)

### Web Hosting

- [Install Apache on CentOS 7](./apache.md)
- [Apache config](./apacheConfig.md)
- **[Install NginX](./nginx.md)**
  - [Setup NginX with Apache](./nginxApache.md)
  - [Setup NginX Proxy Manager](./nginxProxyManager.md)
- **[SSL Certificates](./sslCertificates.md)**
  - [Free Lets Encrypt SLL Certificates](./letsEncryptSSL.md)
- [Install Tomcat Server](./tomcat.md)

### Virtual Hosts

- [Setup Virtual Hosts](./vhosts/README.md)
- [Directory Structure](./vhosts/structure.md)
- [Permissions](./vhosts/permissions.md)
- [demoPages](./vhosts/demoPages.md)
- [createConfFiles](./vhosts/createConfFiles.md)
- [hostsFile](./vhosts/hostsFile.md)

### WebDav Setup with Apache

- [WebDav Setup](./webdav/README.md)

### Container Management

- [Docker](./docker/README.md)
- [Install Docker](./docker/installDocker.md)
- [Install Portainer for Containers](./portainer.md)
- [Docker Compose via Portainer](./codeServerDocker.md)
- [Install LazyDocker via GO](./lazyDocker.md)

### System

- [Set Resource Limit on Process / Service](./limitProcessResources.md)
- [Install CWP Control Panel](./cwp.md) - Do not install
- [Install Cockpit Server Management](./cockpit.md)
- [Install dutree](./dutree.md)
 
### File Management

- [Install Double Commander](./doublecommander.md)
- [Install Cloud Commander](./cloudCommander.md)
- [Install Droppy](./droppy.md)
- [Install Samba](./samba.md)

### Databases

- [Install CouchDB](./couchDB.md)
- [Install Mongo DB](./mongodb.md)
- [Install PostgreSQL](./postgreSQL.md)
- [Install Redis](./redis.md)

### Dashboards 

- [Install Heimdal Dashboard](./heimdal.md)
- [Install Flame Dashboard](./flame.md)
- [Install Dash Machine](./dashMachine.md)
- [Install Code Snippets](./codeSnippets.md)

### Development

- [Install Bun CLI v0.14](./bun.md)
- [Install newt `Whiptail`](./newt.md)
- [Install PHP 8](./php8.md)
- [Install Multiple Version of PHP on same server](./phpMulti.md)
- [Install Composer](./composer.md)
- [Install Cloud9 IDE](./cloud9.md)
- [Install Python 3](./python3.md)
- [Install Node.js on CentOS 7](./node.md)
- [Install Node Version Manager](./nvm.md)
- [Install Golang on CentOS 7](./goLang.md)
- [Install Java](./java.md)

### Tools

- [Install Firefox X11 Forwarding](./firefox.md)
- [Install Dillinger for MD](./dillinger.md)
- [Install VS Code-Server 4](./codeServer.md)**
- [Code-Server Extensions](./codeServerExtensions.md)
- [Code-Server as Service](./codeServerService.md)