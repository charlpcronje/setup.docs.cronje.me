# Update TAR

The version of tar that comes it CentOS 7 has a few security updates so it is important to update `tar` before continuing to setup your server,
it is very simple:

## Get Current Version

You cam have a look at your version of tar like this

```shell
tar --version

# Output
# tar (GNU tar) 1.26
# Copyright (C) 2011 Free Software Foundation, Inc.
# License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>.
# This is free software: you are free to change and redistribute it.
# There is NO WARRANTY, to the extent permitted by law.
```

## Update `tar`

```shell
sudo yum update tar

# Output
# Loading mirror speeds from cached hostfile
# * base: mirror.web-ster.com
# * epel: mirrors.kernel.org
# * extras: repo1.sea.innoscale.net
# * updates: mirror.web-ster.com
# No packages marked for update
```
