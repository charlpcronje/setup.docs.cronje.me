---
title: How to Install Python 3 on CentOS 7.7 using yum/source and set as Default
label: How to Install Python 3 on CentOS 7.7
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


- The CentOS 7 Linux distribution includes Python 2 by default. However, Python 2 has reached its EOL on January 1, 2020.
- In this tutorial, we are going to take a look at how to get up and running with Python 3 on a CentOS 7 server.
- These instructions assume that your server has CentOS release 7.7.

## Yum Installation

- In CentOS 7 releases prior to 7.7, it was necessary to make Python 3 available for installation by setting up third-party repositories, such as the IUS repository, because the CentOS base repository did not provide a Python 3 package. Thankfully, as of CentOS 7.7, Python 3 is available in the base package repository!

### Step 1: Update the environment

```sh
[root@centos7 ~]# yum update -y

```

### Step 2: Install Python 3

```sh
[root@centos7 ~]# yum install -y python3
```

That’s it! Python 3 is now installed! Another helpful idea to consider is that PIP, the Python package manager for Python 3, is installed alongside the Python 3 package, so we don’t have to worry about that as an additional installation step.

### Step 3: Setup the Environment

- Install development tools and some prerequisite packages.

```sh
[root@centos7 ~]# yum groupinstall -y "Development Tools" && yum install gcc openssl-devel bzip2-devel libffi-devel -y
```

### Step 4: Set Python 3 as default

```sh
[root@centos7 ~]# alternatives --install /usr/bin/python python /usr/bin/python2 50
[root@centos7 ~]# alternatives --install /usr/bin/python python /usr/bin/python3.6 60
[root@centos7 ~]# alternatives --config python
```

### Verify Installation

In order to ensure that Python 3 is in fact installed and useable, we can drop into a Python 3 shell by running the following command.

```sh
[root@centos7 ~]# python
Python 3.6.8 (default, Aug  7 2019, 17:28:10) 
[GCC 4.8.5 20150623 (Red Hat 4.8.5-39)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```
You should see the version of Python 3 installed on your system as well as a change in the command prompt characters.

### Fix for Yum install Errors

Yum package manager usage python2 by default so after you make python3 as default the yum will break.

```sh
[root@centos7 ~]# yum install ftp
  File "/usr/bin/yum", line 30
    except KeyboardInterrupt, e:
                            ^
SyntaxError: invalid syntax
Fix it here -
```

To fix this change the python interpreter to `/usr/bin/python2.7` in two files

```sh
[root@centos7 ~]# cat /usr/bin/yum
#!/usr/bin/python2.7
[root@centos7 ~]# cat /usr/libexec/urlgrabber-ext-down
#!/usr/bin/python2.7
```

## Source Installation

- Installing Python 3 via the Yum package manager is by far the simplest way to get the job done. However, in some cases, you might want to have the most recent version of Python available and that’s where a source installation can come in handy.

### Step 1: Setup the Environment
- In order to install Python 3 from source, we are going to need to ensure that some prerequisite packages are installed on our system.

```sh
[root@centos7 ~]# yum install gcc openssl-devel bzip2-devel libffi-devel -y
```

### Step 2: Download Python

Next, we need to grab the version of Python we want. The following command will pull down the latest stable version of Python 3.8 as of the writing of this article.

```sh
[root@centos7 ~]# curl -O https://www.python.org/ftp/python/3.8.1/Python-3.8.1.tgz
```

Now we need to extract the file.

```sh
[root@centos7 ~]# tar -xzf Python-3.8.1.tgz
```

### Step 3: Install Python 3

Now that it’s extracted, let’s change into the resultant directory.

```sh
[root@centos7 ~]# cd Python-3.8.1/
```

Next, we need to prepare to compile Python from source.

```sh
[root@centos7 Python-3.8.1]# ./configure --enable-optimizations
```

Finally, we are going to use the following command to finish off the installation, without replacing the default system Python on our system.

```sh
[root@centos7 Python-3.8.1]# make altinstall
```

Compiling code from source takes a little while, but once that’s finished, we can test out our new Python 3 version by running the following command.

```sh
[root@centos7 Python-3.8.1]# python3.8
```

- Much like before when we installed Python 3.6 via Yum, we are dropped into a Python shell that outputs the version we are currently using.
- Python 3.8.1 (default, Dec 27 2019, 17:12:30)

```sh
[GCC 4.8.5 20150623 (Red Hat 4.8.5-39)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>
``

Done