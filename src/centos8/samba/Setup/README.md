---
title: Introduction
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


Composer is a tool for dependency management in PHP. It allows you to declare the libraries your project depends on and it will manage (`install/update`) them for you.

## Dependency management

Composer is not a package manager in the same sense as Yum or Apt are. Yes, it deals with "packages" or libraries, but it manages them on a per-project basis, installing them in a directory (e.g. vendor) inside your project. By default, it does not install anything globally. Thus, it is a dependency manager. It does however support a "global" project for convenience via the global command.

This idea is not new and Composer is strongly inspired by node's npm and ruby's bundler.

_Suppose:_

You have a project that depends on a number of libraries.
Some of those libraries depend on other libraries.
Composer:

> Enables you to declare the libraries you depend on. Finds out which versions of which packages can and need to be installed, and installs them (meaning it downloads them into your project).

You can update all your dependencies in one command.
See the Basic usage chapter for more details on declaring dependencies.

## System Requirements

Composer requires `PHP 5.3.2+` to run. A few sensitive php settings and compile flags are also required, but when using the installer you will be warned about any incompatibilities.

To install packages from sources instead of plain zip archives, you will need git, svn, fossil or hg depending on how the package is version-controlled.

Composer is multi-platform and we strive to make it run equally well on Windows, Linux and macOS.

### Installation - Linux / Unix / macOS

Downloading the Composer Executable#
Composer offers a convenient installer that you can execute directly from the command line. Feel free to download this file or review it on GitHub if you wish to know more about the inner workings of the installer. The source is plain PHP.

There are in short, two ways to install Composer. Locally as part of your project, or globally as a system wide executable.

### Locally

To install Composer locally, run the installer in your project directory. See the Download page for instructions.

The installer will check a few PHP settings and then download composer.phar to your working directory. This file is the Composer binary. It is a `PHAR` (`PHP archive`), which is an archive format for PHP which can be run on the command line, amongst other things.

Now run `php composer.phar` in order to run Composer.

You can install Composer to a specific directory by using the `--install-dir` option and additionally (re)name it as well using the `--filename option`. When running the installer when following the Download page instructions add the following parameters:

```CMD
php composer-setup.php --install-dir=bin --filename=composer
```

Now run php bin/composer in order to run Composer.

### Globally

You can place the Composer PHAR anywhere you wish. If you put it in a directory that is part of your PATH, you can access it globally. On Unix systems you can even make it executable and invoke it without directly using the php interpreter.

After running the installer following the Download page instructions you can run this to move composer.phar to a directory that is in your path:

`mv composer.phar /usr/local/bin/composer`

If you like to install it only for your user and avoid requiring root permissions, you can use ~/.local/bin instead which is available by default on some Linux distributions.

_Note:_ If the above fails due to permissions, you may need to run it again with sudo.

Note: On some versions of macOS the `/usr` directory does not exist by default. If you receive the error "`/usr/local/bin/composer:` No such file or directory" then you must create the directory manually before proceeding: `mkdir -p /usr/local/bin`.

Note: For information on changing your PATH, please read the Wikipedia article and/or use your search engine of choice.

Now run composer in order to run Composer instead of php composer.phar.

## Installation - Windows

### Using the Installer

This is the easiest way to get Composer set up on your machine.

Download and run `Composer-Setup.exe`. It will install the latest Composer version and set up your PATH so that you can call composer from any directory in your command line.

Note: Close your current terminal. Test usage with a new terminal: This is important since the PATH only gets loaded when the terminal starts.

### Manual Installation

Change to a directory on your PATH and run the installer following the Download page instructions to download composer.phar.

Create a new composer.bat file alongside composer.phar:

Using `cmd.exe`:

```CMD
C:\bin> echo @php "%~dp0composer.phar" %*>composer.bat
```

### Using PowerShell

```PS
PS C:\bin> Set-Content composer.bat '@php "%~dp0composer.phar" %*'
```

> Add the directory to your PATH environment variable if it isn't already. For information on changing your PATH variable, please see this article and/or use your search engine of choice.

Close your current terminal. Test usage with a new terminal:

```CMD
C:\Users\username>composer -V
Composer version 2.0.12 2021-04-01 10:14:59
```

### Using Composer

Now that you've installed Composer, you are ready to use it! Head on over to the next chapter for a short demonstration.