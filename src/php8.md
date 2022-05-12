# Install PHP 8 on CentOS/RHEL 8/7

## Step 1: Enable EPEL and Remi Repository on CentOS/RHEL

Right off the bat, you need to enable the EPEL repository on your system. EPEL, short for Extra Packages for Enterprise Linux, is an effort from the Fedora team that provides a set of additional packages that are not present by default on RHEL & CentOS.

```shell
sudo dnf install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm  [On CentOS/RHEL 8]
```

Remi repository is a third-party repository that provides a wide range of PHP versions for RedHat Enterprise Linux. To install the Remi repository, run the command:

```shell
sudo dnf install -y https://rpms.remirepo.net/enterprise/remi-release-8.rpm  [On CentOS/RHEL 8]
```

## Step 2: Install PHP 8 on CentOS/RHEL

Once the installation is complete, proceed and list the available php module streams as shown:

```shell
# CentOS 7:

sudo yum -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
sudo yum -y install https://rpms.remirepo.net/enterprise/remi-release-7.rpm
sudo yum -y install yum-utils
sudo yum-config-manager --disable 'remi-php*'
sudo yum-config-manager --enable remi-php80
sudo yum -y install php php-{cli,fpm,mysqlnd,zip,devel,gd,mbstring,curl,xml,pear,bcmath,json}

# Update 2022-01-26 this is what worked last for me to upgrade to php 8
yum-config-manager --enable remi-php80
yum install php php-mcrypt php-cli php-gd php-curl php-mysql php-ldap php-zip php-fileinfo
```

```shell
# CentOS 8
sudo dnf -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
sudo dnf -y install https://rpms.remirepo.net/enterprise/remi-release-8.rpm
sudo dnf -y install yum-utils
sudo dnf module reset php
sudo dnf install php80
```
