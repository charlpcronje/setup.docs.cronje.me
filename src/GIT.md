---
title: Install GIT on CentOS 7
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>

Use yum, `CentOS’s` native `package manager`, to search for and install the latest git package available in `CentOS’s` repositories:

## Install Using `Yum`

```shell
sudo yum install git
```

If the command completes without error, you will have git downloaded and installed. To double-check that it is working correctly, try running Git’s built-in version check:

```shell
git --version
```

Now I'm creating a config.etc repo on my GitHub Account.

## Setup SSH Key for Github

```shell
ssh-keygen -t rsa -b 2048 -C "charlcp@gmail.com"

cd ~
cd .ssh
cat id_rsa.pub
```

- Select and copy the key contents
- Go to [github.com](github.com)
- Click on settings
- Click SSH and PGP Keys
- Click on new key
- Paste key and give it a name
- Click save

---
> Done

## Upgrading GIT

### Remove old git

```shell
sudo yum -y remove git
sudo yum -y remove git-*
```

### Add End Point CentOS 7 repo

The quickest way of installing the latest version of Git on CentOS 7 is from the End Point repository.

```shell
sudo yum -y install https://packages.endpoint.com/rhel/7/os/x86_64/endpoint-repo-1.9-1.x86_64.rpm
```

Once repository is added, install Git 2.x on CentOS 7

```shell
sudo yum install git
```

Check git version after installing git2u-all package

```shell
git --version
# git version 2.34.1 - At the time of writing this doc 2022-01-16
```
