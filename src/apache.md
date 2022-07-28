---
title: Installing Apache on CentOS 7
label: Installing Apache on CentOS 7
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


## Step 1: Update Software Versions List

Ensure you are using the latest versions of the software. In a terminal window, input the command:

```shell
sudo yum update
```

The system should reach out to the software repositories and refresh the list to the latest versions.

## Step 2: Install Apache

To install Apache on your CentOS server, use the following command:

```shell
sudo yum install httpd
```

The system should download and install the Apache software packages.

## Step 3: Activate Apache

To activate Apache, start its service first.

1. Enter the following command in a terminal window:

```shell
sudo systemctl start httpd
```

This will start the Apache service.

1. Next, set the Apache service to start when the system boots:

```shell
sudo systemctl enable httpd
```

## Step 4: Verify Apache Service

Display information about Apache, and verify it’s currently running with:

```shell
sudo systemctl status httpd
```

I got the following message when I did a status check
> AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 127.0.0.1. Set the 'ServerName' d...this message

So from this I gather I should set the server name.

```shell
nano /etc/httpd/conf/httpd.conf
```

verifying the apache service is running

## Step 5: Configure firewalld to Allow Apache Traffic

In a standard installation, CentOS 7 is set to prevent traffic to Apache.

Normal web traffic uses the http protocol on Port 80, while encrypted web traffic uses the https protocol, on Port 443.

1. Modify your firewall to allow connections on these ports using the following commands:

```shell
sudo firewall-cmd ––permanent ––add-port=80/tcp

sudo firewall-cmd ––permanent ––add-port=443/tcp
```

1. Once these complete successfully, reload the firewall to apply the changes with the command:

```shell
sudo firewall-cmd ––reload
```

## Step 6: Configure Virtual Hosts on CentOS 7 (optional)

Virtual hosts are different websites that you run from the same server. Each website needs its own configuration file.

Make sure these configuration files use the .conf extension, and save them in the /etc/httpd/conf.d/ directory.

There are a couple of best practices to use when you’re setting up different websites on the same server:

Try to use the same naming convention for all your websites. For example:

```shell
/etc/httpd/conf.d/MyWebsite.com.conf
/etc/httpd/conf.d/TestWebsite.com.conf
```

Use a different configuration file for each domain. The configuration file is called a vhost, for a virtual host. You can use as many as you need. Keeping them separate makes troubleshooting easier.

1. To create a virtual host configuration file, enter the following into a terminal window:

```shell
sudo vi /etc/httpd/conf.d/vhost.conf
```

This will launch the Vi text editor, and create a new vhost.conf file in the /etc/httpd/conf.d directory.

1. In the editor, enter the following text:

```conf
NameVirtualHost *:80

    <VirtualHost *:80>
    ServerAdmin webmaster@MyWebsite.com
    ServerName MyWebsite.com
    ServerAlias www.MyWebsite.com
    DocumentRoot /var/www/html/MyWebsite.com/public_html/
    ErrorLog /var/www/html/MyWebsite.com/logs/error.log
    CustomLog /var/www/html/MyWebsite.com/logs/access.log combined
</VirtualHost>
```

Save the file and exit.

1. Next, enter the following command to create a directory for you to store your website files in:

```shell
sudo mkdir /var/www/MyWebsite/{public_html, logs}
```

1. Restart the Apache service to apply your changes by entering:

```shell
sudo systemctl restart httpd
```

Once the system finishes, you should be able to open a browser window to MyWebsite.com and see a default Apache test page.

You can replace MyWebsite above with the name of your domain. If you are hosting more than one domain, make sure you create a new directory in /var/www/ for each one. You can copy the code block in your /etc/httpd/conf.d/vhost.conf file, and replace MyWebsite with another domain name that you’re hosting.

Apache Directories and Files
One of the main ways Apache functions is through configuration files. They are located at /etc/httpd.

Apache has a main configuration file: /etc/httpd/conf/httpd.conf .

If there are any other `configuration files`, they are included in the main configuration file. They should use the `.conf` extension and should be stored in the `/etc/httpd/conf.d/` directory.

You can enhance Apache’s functionality by loading additional modules.

The configuration files for these modules should be stored in: `/etc/httpd/conf.modules.d/` directory.

Log files record all the activity of the Apache service, including client activity on the websites your system is hosting. These logs can be found in:  `/var/log/httpd/`.

Commands For Managing Apache Service
Other commands that you can use to control the Apache service include:

Stop Apache Service:

```shell
sudo systemctl stop httpd
```

Prevent or disable Apache from starting when the system boots:

```shell
sudo systemctl disable httpd
```

Re-enable Apache at boot:

```shell
sudo systemctl enable httpd
```

Restart Apache and apply any changes you have made:

```shell
sudo systemctl restart httpd
```
