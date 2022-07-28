---
title: Install DNF in RHEL/CentOS 7
label: Install DNF in RHEL/CentOS 7
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


DNF stands for Dandified yum. DNF is a software package manager for RPM-based Linux distributions such as Fedora, RHEL and CentOS. It is the next upcoming major version of Yum. DNF is first introduced in Fedora and has replaced to become the default package manager of the Fedora distributions. DNF is same as Yum that installs, updates and removes packages on RPM bas4ed Linux systems. DNF is introduced for improving the bottlenecks of Yum such as performance, Memory usages, Dependency resolution, speed, and some other factors. The latest stable release of DNF is 1.0 and it is written in Python.

To install DNF on RHEL/CentOS 7 systems, you need to set up and enable epel YUM REPO before installing DNF.

## Install EPEL

```shell
yum install epel-release
```

## Install DNF

```shell
yum install dnf
```

## Using DNF

You can now start to run commands using DNF. To view the man page you can use the following command:

```shell
dnf –help
```

## DNF vs YUM command Examples

1. Install a Package

```shell
YUM: yum install <package>
```

Eg: yum install httpd

```shell
DNF: dnf install <package>
```

```shell
Eg: dnf install httpd
```

## Upgrade a package

```shell
YUM: yum upgrade <package>
```

```shell
Eg: yum update mysql-server
```

```shell
DNF: dnf upgrade <package>
```

```shell
Eg: dnf upgrade mysql-server
```

## Remove a package

```shell
YUM: yum remove <package>
```

Eg: yum remove httpd

```shell
DNF: dnf remove <package>
```

```shell
Eg: dnf remove httpd
```

## Advantages of DNF

- DNF comes with a simplified code: DNF has about 29000 lines of code compared to over 59000 in yum.
- Support for multiple repositories.
- Faster and lesser memory intensive operations compared to yum.
- Simple interface.
- DNF runs in both Python 2 and Python 3.
- Simple configuration.
- DNF has faster dependency resolving speed than yum.
- RPM consistent behavior.
- C bindings for lower level libraries.
- Package group support, including multiple-repository groups.

The default location of DNF configuration file is `/etc/dnf/dnf.conf`.

## Available DNF commands

- autoremove
- check-update
- clean
- distro-sync
- downgrade
- group
- help
- history
- info
- install
- list
- makecache
- mark
- provides
- reinstall
- remove
- repolist
- repository-packages
- search
- updateinfo
- upgrade
- upgrade-to
