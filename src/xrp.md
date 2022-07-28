---
title: Install XRDP (Remote Desktop) Server on Centos 8
label: Install XRDP (Remote Desktop) Server on Centos 8
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

XRDP is an open-source implementation of the Microsoft Remote Desktop (RDP) that allows you to graphically control your system. With RDP, you can log in to the remote machine the same as you had logged into the local machine. It uses Port 3389 for its connection. In this tutorial, we will look at how to set up the Remote desktop Connection on Centos 8.

## Installing CentOS Desktop Environment

Generally, Linux Server does not have a remote desktop installed. If you want to connect through a GUI, the first step is to install it. GNOME is the default desktop environment in Centos 8. To install GNOME on your remote machine, open up the terminal and run the following command:

```sh
# dnf groupinstall "Server with GUI"
```

Depending on your system, downloading and install the GNOME packages and dependencies may take some time.

## Installing XRDP

XRDP is available in the EPEL software repository. If EPEL is not enabled on your system, enable it by typing the following command:

```sh
dnf install epel-release
```

Now install the XRDP package.

```sh
dnf install xrdp
```

Once the installation is complete enable and start the XRDP service.

```
# systemctl enable xrdp
# systemctl start xrdp
```

To verify the XRDP is running, type the following command:

```
# systemctl status xrdp
```

If the XRDP service is running, the output should be like this as shown in the figure below:

![terminal1](./xrdp/xrdp1.webp)

You can also verify the XRDP service state by using the following command:

```
# netstat –atnp | grep 3389
```

![terminal2](./xrdp/xrdp2.webp)

Port should be Listening like below:

![terminal3](./xrdp/xrdp3.webp)

## Configuring XRDP

The configuration file is **/etc/xrdp/xrdp.ini**. By default, XRDP uses windows desktop, which is in our case is GNOME. For the connection, you don’t need to make any changes in the configuration file. This file is divided into different sections and allows you to set global configuration settings such as security and listening address and you can also create different XRDP login sessions.

Open up configuration file **/etc/xrdp/xrdp.ini** and add the following line at the end of the file.

```
exec gnome-session
```

After adding the above line restart the XRDP service, using the following command:

```
# systemctl restart xrdp
```

## Configure the Firewall

If your firewall is running on your Centos 8, just add the rule to allow the XRDP port/service to allow traffic for the XRDP connection.

```
# firewall-cmd --add-port = 3389/tcp -- permanent

# firewall-cmd –reload
```

## Connecting to the XRDP using Windows Machine

Windows by default uses a remote desktop client. To connect through Centos 8 using remote desktop type **Remote desktop connection** in the windows search bar and press enter.

![terminal4](./xrdp/xrdp4.webp)

Enter the IP address of the remote machine and click on connect.

![terminal5](./xrdp/xrdp5.webp)

It will prompt you to the login screen for the credentials. Enter **username and password** and click on **Ok**.

![terminal6](./xrdp/xrdp6.webp)

Once logged in, you should see the default GNOME Desktop. Now you can start interacting with the remote machine.

If you are using Mac OS, install the Microsoft Remote Desktop application from Mac App Store, whereas the Linux user can use RDP clients like **Remmina** or **Vinagre**.