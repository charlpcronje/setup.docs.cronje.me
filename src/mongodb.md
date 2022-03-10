# Install MongoDB Community Edition on Centos 7

## MongoDB Version

This tutorial installs MongoDB 5.0 Community Edition. To install a different version of MongoDB Community, use the version drop-down menu in the upper-left corner of this page to select the documentation for that version.

Follow these steps to install MongoDB Community Edition using the yum package manager.

## Configure the package management system (yum)

Create a `/etc/yum.repos.d/mongodb-org-5.0.repo` file so that you can install MongoDB directly using yum:

```shell
[mongodb-org-5.0]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/5.0/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-5.0.asc
```

You can also download the `.rpm` files directly from the `MongoDB` repository. Downloads are organized by Red Hat / CentOS version `(e.g. 7)`, then `MongoDB` release version `(e.g. 5.0)`, then architecture `(e.g. x86_64)`.

Prior to `MongoDB 5.0`, odd-numbered `MongoDB` release versions, such as `4.3`, were development releases. Beginning with `MongoDB` 5.1, `MongoDB` has quarterly rapid releases. For more information on the differences between rapid and long-term support releases, see `MongoDB` Versioning.

## Install the MongoDB packages

```shell
sudo yum install -y mongodb-org
```

## Run MongoDB Community Edition

### Directory Paths

### To Use Default `Directories

By default, `MongoDB` runs using the `mongod` user account and uses the following default directories:

- `/var/lib/mongo` (the data directory)
- `/var/log/mongodb` (the log directory)

## To Use Non-Default Directories

To use a data directory and/or log directory other than the default directories:

### Create the new directory or directories

Edit the configuration file `/etc/mongod.conf` and modify the following fields accordingly:

- `storage.dbPath` to specify a new data directory path (`e.g. /some/data/directory`)
- `systemLog.path` to specify a new log file path (e.g. `/some/log/directory/mongod.log`)
- Ensure that the user running MongoDB has access to the directory or directories:

```shell
sudo chown -R mongod:mongod <directory>
```

If you change the user that runs the MongoDB process, you must give the new user access to these directories.

### Permit Access to netstat for FTDC

The current SELinux Policy does not allow the MongoDB process to open and read /proc/net/netstat, which is required for Full Time Diagnostic Data Capture (FTDC). If you intend to run SELinux in enforcing mode, you will need to make the following adjustment to your SELinux policy:

Ensure your system has the checkpolicy package installed:

```shell
sudo yum install checkpolicy
```

Create a custom policy file `mongodb_proc_net.te`:

```shell
cat > mongodb_proc_net.te <<EOF
module mongodb_proc_net 1.0;
require {
        type sysctl_net_t;
        type mongod_t;
        class dir search;
        class file { getattr open read };
}
#============= mongod_t ==============
#!!!! This avc is allowed in the current policy
allow mongod_t sysctl_net_t:dir search;
allow mongod_t sysctl_net_t:file open;
#!!!! This avc is allowed in the current policy
allow mongod_t sysctl_net_t:file { getattr read };
EOF
```

Once created, compile and load the custom policy module by running these three commands:

```shell
- checkmodule -M -m -o mongodb_proc_net.mod mongodb_proc_net.te
- semodule_package -o mongodb_proc_net.pp -m mongodb_proc_net.mod
- sudo semodule -i mongodb_proc_net.pp
```

### Using a Custom MongoDB Directory Path

Update the SELinux policy to allow the mongod service to use the new directory:

```shell
sudo semanage fcontext -a -t <type> </some/MongoDB/directory.*>
```

where specify one of the following types as appropriate:

```shell
mongod_var_lib_t for data directory
mongod_log_t for log file directory
mongod_var_run_t for pid file directory
```

> NOTE
> Be sure to include the .* at the end of the directory.

Update the SELinux user policy for the new directory:

```shell
sudo chcon -Rv -u system_u -t <type> </some/MongoDB/directory>
```

where specify one of the following types as appropriate:

- `mongod_var_lib_t` for data directory
- `mongod_log_t` for log directory
- `mongod_var_run_t` for pid file directory

Apply the updated SELinux policies to the directory:

```shell
sudo restorecon -R -v </some/MongoDB/directory>
```

## Start MongoDB

You can start the mongod process by issuing the following command:

```shell
sudo systemctl start mongod
```

If you receive an error similar to the following when starting mongod:

```shell
Failed to start mongod.service: Unit mongod.service not found.
```

Run the following command first:

```shell
sudo systemctl daemon-reload
```

Then run the start command above again.

Verify that MongoDB has started successfully.
You can verify that the mongod process has started successfully by issuing the following command:

```shell
sudo systemctl status mongod
```

You can optionally ensure that MongoDB will start following a system reboot by issuing the following command:

```shell
sudo systemctl enable mongod
```

### Stop MongoDB

As needed, you can stop the mongod process by issuing the following command:

```shell
sudo systemctl stop mongod
```

### Restart MongoDB

You can restart the mongod process by issuing the following command:

```shell
sudo systemctl restart mongod
```

You can follow the state of the process for errors or important messages by watching the output in the /var/log/mongodb/mongod.log file.

### Begin using MongoDB

Start a mongosh session on the same host machine as the mongod. You can run mongosh without any command-line options to connect to a mongod that is running on your localhost with default port 27017.

```shell
mongosh
```

For more information on connecting using mongosh, such as to connect to a mongod instance running on a different host and/or port, see the mongosh documentation.

To help you start using MongoDB, MongoDB provides Getting Started Guides in various driver editions. For the driver documentation, see Start Developing with MongoDB.

### Uninstall MongoDB Community Edition

To completely remove MongoDB from a system, you must remove the MongoDB applications themselves, the configuration files, and any directories containing data and logs. The following section guides you through the necessary steps.

> This process will completely remove MongoDB, its configuration, and all databases. This process is not reversible, so ensure that all of your configuration and data is backed up before proceeding.

## MongoDB Stop

Stop the mongod process by issuing the following command:

```shell
sudo service mongod stop
```

### Remove Packages

Remove any MongoDB packages that you had previously installed.

```shell
sudo yum erase $(rpm -qa | grep mongodb-org)
```

### Remove Data Directories

Remove MongoDB databases and log files.

```shell
sudo rm -r /var/log/mongodb
sudo rm -r /var/lib/mongo
```
