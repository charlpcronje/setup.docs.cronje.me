---
title: Installing PHP Composer on CentOS 7
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


## Prerequisites

- A CentOS Linux system
- PHP 5.3.2 or later installed
- A user account with sudo privileges
- Access to a command line/terminal window `(Ctrl+Alt+F2)`

## Step 1: Update Local Repository

Before you download and install anything on your system, make sure always to update the local repository:

```shell
sudo yum -y update
```

## Step 2: Install Software Dependencies

Start with installing the supporting software. Type the following command in the terminal:

```shell
yum install php-cli php-zip wget unzip
```

If you already have the required dependencies, make sure they are the latest version of the package.

install supporting software for composer for centos 7

## Step 3: Download Composer Installer Script

Next, you’ll need to download the installer script. The following command downloads the file in the directory you’re currently in.

```shell
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
```

download composer installer

## Step 4: Verify Integrity of the Download

Once you have the installer script, you’ll need to verify its integrity.

To do so, you need to check whether the SHA-384 hash matches the Installer Signature (SHA-384) found on the official Composer Public Keys page.

Download the authorized signature from Composer’s Github page in the HASH variable:

```shell
HASH="$(wget -q -O - https://composer.github.io/installer.sig)"
```

Then, use the following script to compare the official hash against the one you’ve downloaded:

```shell
php -r "if (hash_file('SHA384', 'composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
```

If the two signatures match, the output shows the message: Installer verified.

On the other hand, if the script detects some differences, it displays: Installer corrupt. To solve this issue, you’ll need to re-download the Composer Installer.

## Step 5: Install Composer

After verifying the integrity of the file you can move on to installing Composer.

You’ll want to install Composer in the `/usr/local/bin directory`, as a command accessible from the whole system.

### 1. To install composer, use the command

```shell
php composer-setup.php --install-dir=/usr/local/bin --filename=composer
```

Once the installation has been initialized, the following message will appear:

```shell
All settings correct for using Composer
Downloading...

Composer (version 1.6.5) successfully installed to: /usr/local/bin/composer
Use it: php /usr/local/bin/composer
```

### 2. When the installer completes the process, check whether it’s running correctly

```shell
composer
```

The system should display the running version, along with its syntax and available options

```shell
   ______
  / ____/___  ____ ___  ____  ____  ________  _____
 / /   / __ \/ __ `__ \/ __ \/ __ \/ ___/ _ \/ ___/
/ /___/ /_/ / / / / / / /_/ / /_/ (__  )  __/ /
\____/\____/_/ /_/ /_/ .___/\____/____/\___/_/
                    /_/
Composer version 1.9.0 2019-08-28 11:45:23

Usage:
  command [options] [arguments]

Options:
  -h, --help                     Display this help message
  -q, --quiet                    Do not output any message
  -V, --version                  Display this application version
      --ansi                     Force ANSI output
      --no-ansi                  Disable ANSI output
  -n, --no-interaction           Do not ask any interactive question
      --profile                  Display timing and memory usage information
      --no-plugins               Whether to disable plugins.
```

### 3. Finally, delete the installer

```shell
php -r “unlink(‘composer-setup.php’);”
```

## Basic Composer Usage

Composer helps track dependencies on a per-project basis, allowing other users to create an identical environment easily. It keeps track of the required software and allowed versions by using a `composer.json` file.

Additionally, it maintains consistency if someone copies the directory through the composer.lock files, which are automatically generated using the require command.

Now, let’s see how to utilize Composer when starting a new PHP project.

1. Open a terminal and create a project root directory for a file with the project description, its dependencies, and other additional information (the `composer.json` file):

```shell
mkdir c_sample
```

1. Then, move it to the new directory:

```shell
cd c_sample
```

1. The next step is loading a package. The website packagist.org has a broad range of different PHP packages to choose from.

In this example, we’ll download and use the monolog/monolog package for our project. The information after the slash is the package name, while the name before the slash is the vendor.

Along with downloading the software, your system will automatically create the composer.json file and the composer.lock file with the command:

composer require monolog/monolog

1. Now, check to see whether all the files were created by listing the content of the directory:

```shell
ls -l
```

Among the content, you should see the composer.json and composer.lock files, as well as a vendor directory.

1. Next, open the composer.json file:

```shell
cat composer.json
```

You should see that the newly added monolog software has a carat (^) sign beside the version number, indicating the minimum version of the software.

### How to Set Up Autoloading

You can simplify working with dependencies by configuring Composer to autoload classes for you (since PHP doesn’t do this automatically).

1. With the text editor of your preference, create a new file (in this example, it will be under the name composer_sample):

```shell
vi composer_sample.php
```

1. Add the following into the file:

```shell
<?php

require __DIR__ . '/vendor/autoload.php';
use Monolog\Logger;
use Monolog\Handler\StreamHandler;

// create a log channel
$log = new Logger('name');
$log->pushHandler(new StreamHandler('/~/c_sample/text.log', Logger::WARNING));

// add records to the log
$log->warning('Foo');
$log->error('Bar');
```

configure composer to autoload

1. Save and exit.

1. With this, you can use the following command to autoload monolog:

```shell
php composer_sample.php
```

### Update Dependencies

If you need to update all the dependencies in your composer.json file you can do so with:

```shell
composer update
```

This command updates dependencies according to the version specified in the file.

You can also update one (or more) dependencies individually:

```shell
composer update vendor/package vendor_b/package_b
```
