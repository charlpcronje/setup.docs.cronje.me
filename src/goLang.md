---
title: Install Golang on CentOS 7
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>

## Prerequisites

The user used(Linux user)In this tutorial is root or a user with root power i.e add sudo at the starting of every command.

## Installing Golang Installer

Follow the below steps to install the Go programming language on Centos 7:

**Step 1**: This is yet another method to get Golang installed on your CentOS 7 / RHEL 7 system. It involves downloading the official Golang Installers for Linux systems as below.

```shell
wget https://storage.googleapis.com/golang/getgo/installer_linux
```

**Step 2**: With the installer downloaded, make it executable.

```shell
sudo chmod +x ./installer_linux
```

**Step 3**: Now run the installer to install the latest Golang version.

```shell
./installer_linux 
```

The installation will proceed as below:

```shell
Welcome to the Go installer!
Downloading Go version go1.17.3 to /home/thor/.go
This may take a bit of time...
Downloaded!
Setting up GOPATH
**GOPATH has been set up!**

One more thing! Run `source /home/thor/.bash_profile` to persist the
new environment variables to your current session, or open a
new shell prompt.
```

You will then be required to source the `~/.bash_profile`

```shell
source ~/.bash_profile
```

Finally, verify the installed version of Golang.

```shell
go version
# go version go1.17.3 linux/amd64
```

**Step 4**: To verify that go is properly installed run this command:

```shell
go version
``
