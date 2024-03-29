---
title: Install Multiple Version of PHP on same server
label: Install Multiple Version of PHP on same server
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


## Prerequisites

Remove all versions of php, Make sure to back up any configuration files.

```sh
dnf remove php php-fpm -y
```

Then remove the rest of the package extensions.

```sh
sudo dnf remove php* -y
```


## Step 1 — Installing PHP Versions 7.4 and 8.1 with PHP-FPM

With the prerequisites completed, you will now install PHP versions 7.4 and 8.1, as well as PHP-FPM and several additional extensions. In order to install multiple versions of PHP, you will need to install and enable the Remi repository to your system. Which also offers the latest versions of the PHP stack on CentOS 8 system.

You can add the both repository to your system using the below commands:

```sh
sudo dnf install http://rpms.remirepo.net/enterprise/remi-release-8.rpm

```

Copy

The command above will also enable the EPEL repository.

First let’s discover what versions of PHP 7 are available on Remi:

```sh
sudo dnf module list php
```

Copy

You’ll see an output like this:

```sh
OutputRemi's Modular repository for Enterprise Linux 8 - x86_64
Name                     Stream                       Profiles                                       Summary                                   
php                      remi-7.2                     common [d], devel, minimal                     PHP scripting language                    
php                      remi-7.4                     common [d], devel, minimal                     PHP scripting language                    
php                      remi-8.1                     common [d], devel, minimal                     PHP scripting language                    
```

Next, disable the default PHP module and enable Remi’s PHP7.4 module using the below command:

```sh
sudo dnf module reset php
sudo dnf module enable php:remi-7.4
```

Lets start to installing `php74` and `php74-php-fpm`:

```sh
sudo dnf install php74 php74-php-fpm -y
```

Install most uses extensions

```sh
sudo dnf install php-cli php-fpm php-curl php-mysqlnd php-gd php-opcache php-zip php-intl php-common php-bcmath php-imap php-imagick php-xmlrpc php-json php-readline php-memcached php-redis php-mbstring php-apcu php-xml php-simplexml php-mysqlnd php-pdo php-mysql
```


- `php74` is a metapackage that can be used to run PHP application.
- `php74-php-fpm` provides the Fast Process Manager interpreter that runs as a daemon and receives Fast/CGI requests.

Now repeat the process for PHP version 8.1. Install `php81` and `php81-php-fpm`.

```
sudo dnf module reset php
sudo dnf module enable php:remi-8.1
sudo dnf install php81 php81-php-fpm -y

```

Install most uses extensions

```sh
sudo dnf install php-cli php-fpm php-curl php-mysqlnd php-gd php-opcache php-zip php-intl php-common php-bcmath php-imap php-imagick php-xmlrpc php-json php-readline php-memcached php-redis php-mbstring php-apcu php-xml php-simplexml php-mysqlnd php-pdo php-mysql
```

After installing both PHP versions, start the `php74-php-fpm` service and enable it to start at boot with the following commands:

```
sudo systemctl start php74-php-fpm
sudo systemctl enable php74-php-fpm

```

Copy

Next, verify the status of `php74-php-fpm` service with the following commands:

```
sudo systemctl status php74-php-fpm

```

Copy

You’ll see the following output:

```
● php74-php-fpm.service - The PHP FastCGI Process Manager
   Loaded: loaded (/usr/lib/systemd/system/php74-php-fpm.service; enabled; vendor preset: disabled)
   Active: active (running) since Wed 2020-04-22 05:14:46 UTC; 52s ago
 Main PID: 14206 (php-fpm)
   Status: "Processes active: 0, idle: 5, Requests: 0, slow: 0, Traffic: 0req/sec"
    Tasks: 6 (limit: 5059)
   Memory: 25.9M
   CGroup: /system.slice/php74-php-fpm.service
           ├─14206 php-fpm: master process (/etc/opt/remi/php74/php-fpm.conf)
           ├─14207 php-fpm: pool www
           ├─14208 php-fpm: pool www
           ├─14209 php-fpm: pool www
           ├─14210 php-fpm: pool www
           └─14211 php-fpm: pool www

Apr 22 05:14:46 centos-s-1vcpu-1gb-nyc3-01 systemd[1]: Starting The PHP FastCGI Process Manager...
Apr 22 05:14:46 centos-s-1vcpu-1gb-nyc3-01 systemd[1]: Started The PHP FastCGI Process Manager.
```

Repeating this process, now start the `php81-php-fpm` service and enable it to start at boot with the following commands:

```
sudo systemctl start php81-php-fpm
sudo systemctl enable php81-php-fpm
```



And then verify the status of `php81-php-fpm` service with the following commands:

```
sudo systemctl status php81-php-fpm
```

You’ll see the following output:

```
● php81-php-fpm.service - The PHP FastCGI Process Manager
   Loaded: loaded (/usr/lib/systemd/system/php81-php-fpm.service; enabled; vendor preset: disabled)
   Active: active (running) since Wed 2020-04-22 05:16:16 UTC; 23s ago
 Main PID: 14244 (php-fpm)
   Status: "Processes active: 0, idle: 5, Requests: 0, slow: 0, Traffic: 0req/sec"
    Tasks: 6 (limit: 5059)
   Memory: 18.8M
   CGroup: /system.slice/php81-php-fpm.service
           ├─14244 php-fpm: master process (/etc/opt/remi/php81/php-fpm.conf)
           ├─14245 php-fpm: pool www
           ├─14246 php-fpm: pool www
           ├─14247 php-fpm: pool www
           ├─14248 php-fpm: pool www
           └─14249 php-fpm: pool www

Apr 22 05:16:15 centos-s-1vcpu-1gb-nyc3-01 systemd[1]: Starting The PHP FastCGI Process Manager...
Apr 22 05:16:16 centos-s-1vcpu-1gb-nyc3-01 systemd[1]: Started The PHP FastCGI Process Manager.

```

At this point you have installed two PHP versions on your server. Next, you will create a directory structure for each website you want to deploy.

## Step 2 — Creating Directory Structures for Both Websites

In this section, you will create a document root directory and an index page for each of your two websites.

First, create document root directories for both site1.your\_domain and site2.your\_domain:

```
sudo mkdir /var/www/site1.your_domain
sudo mkdir /var/www/site2.your_domain

```

By default, Apache webserver runs as a apache user and apache group. To ensure that you have the correct ownership and permissions of your website root directories, execute the following commands:

```
sudo chown -R apache:apache /var/www/site1.your_domain
sudo chown -R apache:apache /var/www/site2.your_domain
sudo chmod -R 755 /var/www/site1.your_domain
sudo chmod -R 755 /var/www/site2.your_domain

```

The `chown` command changes the ownership of your two website directories to the `apache` user and the `apache` group. The `chmod` command changes the permissions associated with that user and group, as well as others.

Next you will create an `info.php` file inside each website root directory. This will display each website’s PHP version information. Begin with site1:

```
sudo vi /var/www/site1.your_domain/info.php

```

Add the following line:

/var/www/<^>site1.your\_domain<^>/info.php

```
<?php phpinfo(); ?>
```

Save and close the file. Now copy the info.php file you created to site2:

```
sudo cp /var/www/site1.your_domain/info.php /var/www/site2.your_domain/info.php
```

Your web server now has the document root directories that each site requires to serve data to visitors. Next, you will configure your Apache web server to work with two different PHP versions.

## Step 3 — Configuring Apache for Both Websites

In this section, you will create two virtual host configuration files. This will enable your two websites to work simultaneously with two different PHP versions.

In order for Apache to serve this content, it is necessary to create a virtual host file with the correct directives. You’ll create two new virtual host configuration file inside the directory `/etc/httpd/conf.d/`.

First create a new virtual host configuration file for the website site1.your\_domain. Here you will direct Apache to render content using `php7.4`:

```
sudo vi /etc/httpd/conf.d/site1.your_domain.conf
```

Add the following content. Make sure the website directory path, server name, and PHP version match your setup:

/etc/httpd/conf.d/site1.your\_domain.conf

```
<VirtualHost *:80>
     ServerAdmin admin@site1.your_domain
     ServerName site1.your_domain
     DocumentRoot /var/www/site1.your_domain
     DirectoryIndex info.php
     ErrorLog /var/log/httpd/site1.your_domain-error.log
     CustomLog /var/log/httpd/site1.your_domain-access.log combined

  <IfModule !mod_php7.c>
    <FilesMatch \.(php|phar)$>
        SetHandler "proxy:unix:/var/opt/remi/php74/run/php-fpm/www.sock|fcgi://localhost"
    </FilesMatch>
  </IfModule>

</VirtualHost>
```

For `DocumentRoot` you are specifying the path of your website root directory. For `ServerAdmin` you are adding an email that the `your_domain` site administrator can access. For `ServerName` you are adding the url for your first subdomain. For SetHandler you are specifying the PHP-FPM socket file for php7.4.

Save and close the file.

Next, create a new virtual host configuration file for the website site2.your\_domain. You will specify this subdomain to deploy `php8.1`:

```
sudo vi /etc/httpd/conf.d/site2.your_domain.conf
```

Copy

Add the following content. Again, make sure the website directory path, server name, and PHP version match your unique information:

/etc/httpd/conf.d/site2.your\_domain.conf

```
<VirtualHost *:80>
     ServerAdmin admin@site2.your_domain
     ServerName site2.your_domain
     DocumentRoot /var/www/site2.your_domain
     DirectoryIndex info.php
     ErrorLog /var/log/httpd/site2.your_domain-error.log
     CustomLog /var/log/httpd/site2.your_domain-access.log combined
  <IfModule !mod_php7.c>
    <FilesMatch \.(php|phar)$>
        SetHandler "proxy:unix:/var/opt/remi/php81/run/php-fpm/www.sock|fcgi://localhost"
    </FilesMatch>
  </IfModule>

</VirtualHost>
```

Save and close the file when you are finished. Then, check the Apache configuration file for any syntax errors with the following command:

```
sudo apachectl configtest
```

You’ll see an output printing `Syntax OK`:

```
OutputSyntax OK
```

Finally, restart the Apache service to implement your changes:

```
sudo systemctl restart httpd
```

Now that you have configured Apache to serve each site, you will test them to make sure the proper PHP versions are running.

## Step 4 — Testing Both Websites

At this point, you have configured two websites to run two different versions of PHP. Now test the results.

Open your web browser and visit both sites `http://site1.your_domain` and `http://site2.your_domain`. You will see two pages that look like this:

![PHP 7.4 info page](https://assets.digitalocean.com/articles/67125/php74.png) ![PHP 8.1 info page](https://assets.digitalocean.com/articles/67125/php81.png)

Note the titles. The first page indicates that site1.your\_domain deployed PHP version 7.4. The second indicates that site2.your\_domain deployed PHP version 8.1.

Now that you’ve tested your sites, remove the `info.php` files. Because they contain sensitive information about your server and are accessible to unauthorized users, they pose a security vulnerability. To remove both files, run the following commands:

```
sudo rm -rf /var/www/site1.your_domain/info.php
sudo rm -rf /var/www/site2.your_domain/info.php

```

You now have a single CentOS 8 server handling two websites with two different PHP versions. PHP-FPM, however, is not limited to this one application.

There are still a few things that could have gone wrong during the setup that I did not all handle in these docs, but here are some links if you get stuck:

- [https://www.linuxcapable.com/how-to-install-php-8-1-on-centos-8-stream/](https://www.linuxcapable.com/how-to-install-php-8-1-on-centos-8-stream/)
- [https://stackoverflow.com/questions/63080021/php-installation-error-it-is-not-possible-to-switch-enabled-streams-of-a-modul](https://stackoverflow.com/questions/63080021/php-installation-error-it-is-not-possible-to-switch-enabled-streams-of-a-modul)
- [https://www.digitalocean.com/community/tutorials/how-to-run-multiple-php-versions-on-one-server-using-apache-and-php-fpm-on-centos-7](https://www.digitalocean.com/community/tutorials/how-to-run-multiple-php-versions-on-one-server-using-apache-and-php-fpm-on-centos-7)
- [https://stackoverflow.com/questions/66043552/make-php7-and-php-8-live-together](https://stackoverflow.com/questions/66043552/make-php7-and-php-8-live-together)


## Conclusion

You have now combined virtual hosts and PHP-FPM to serve multiple websites and multiple versions of PHP on a single server. The only practical limit on the number of PHP sites and PHP versions that your Apache service can handle is the processing power of your instance.

From here you might consider [exploring PHP-FPM’s more advanced features](https://php-fpm.org/about/), like its adaptive spawning process or how it can log `sdtout` and `stderr`. Alternatively, you could now secure your websites with free TLS/SSL certificates from Let’s Encrypt.