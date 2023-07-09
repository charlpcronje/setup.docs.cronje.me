# limit process resources in Rocky Linux 8.8

To limit process resources in Rocky Linux 8.8, you have several options:

1. Using `systemd-run`:
- `systemd-run` is a system and service manager available in most Linux distros, including Rocky Linux.
- It allows you to add resource limitations directly to a specific process.
- You can launch a process with a specific RAM limitation using the `--scope` option and the `MemoryLimit` parameter:

```sh
systemd-run --scope -p MemoryLimit=1000M ./myProcess.sh
```

- You can also limit the CPU usage of a process by specifying the `CPUQuota` parameter:

```sh
systemd-run --scope -p CPUQuota=10% ./myProcess.sh
```

- To combine both CPU and memory limits, use:

```sh
systemd-run --scope -p MemoryLimit=1000M -p CPUQuota=10% ./myProcess.sh
```

2. Using `ulimit`:
- `ulimit` is a built-in function of the bash shell that allows you to create or overwrite limitations on resources like RAM and disk space.
- You can set a soft limit on RAM usage for all future processes by running:

```sh
ulimit -Sv 1000000
```

- This command sets a soft limit of 1GB of RAM, which will affect all subsequent processes launched by the user.
- To limit the maximum file size created by a process, you can use:

```sh
ulimit -Sf 2000
```

- This limits the file size to 2MB for all processes launched by the user.
- You can combine both RAM and file size limits and immediately launch a process using:

```sh
ulimit -Sv 1000000 -Sf 2000 && ./myProcess.sh
```

3. Using `cpulimit`:
- `cpulimit` is a tool that can limit the CPU usage of new or existing processes.
- You can install `cpulimit` on Rocky Linux by running:

```sh
sudo apt-get install cpulimit
```

- Once installed, you can use `cpulimit` to limit the CPU usage of a specific process by specifying the process ID (PID) and the desired CPU usage percentage:

```sh
cpulimit -p <pid> -l <percentage>
```

- For example, to limit the CPU usage of a process with PID 1234 to 50%, you would run:

```sh
cpulimit -p 1234 -l 50
```

## To limit the resources of a service in Rocky Linux 8.8, you can follow these steps:

1. **Identify the service**: Determine the name of the service you want to limit the resources for. This can be done by checking the running services on your system using the `systemctl` command. For example, to list all running services, you can run:

```sh
systemctl list-units --type=service --state=running
```

This will give you a list of running services, and you can identify the service you want to limit.

2. **Configure resource limits**: Once you have identified the service, you can configure resource limits for it using the `systemd.resource-control` module. This module allows you to set limits on various resources such as CPU, memory, and disk I/O for a specific service.

To set resource limits for a service, you need to create a `.service` drop-in file in the `/etc/systemd/system/<service-name>.service.d/` directory. In this file, you can specify the resource limits using the `CPUQuota`, `MemoryLimit`, and `IOAccounting` directives.

Here's an example of how to set resource limits for a service called `my-service`:

```sh
sudo mkdir /etc/systemd/system/my-service.service.d
sudo nano /etc/systemd/system/my-service.service.d/limits.conf
```

In the `limits.conf` file, you can specify the resource limits. For example, to limit CPU usage to 50% and memory usage to 1GB, you can add the following lines:

```sh
[Service]
CPUQuota=50%
MemoryLimit=1G
```

Save the file and exit the editor.

3. **Reload systemd and restart the service**: After configuring the resource limits, you need to reload the systemd configuration and restart the service for the changes to take effect. Run the following commands:

```
sudo systemctl daemon-reload
sudo systemctl restart <service-name>
```

Replace `<service-name>` with the actual name of the service you want to limit.

The service will now be limited to the specified resource limits.

It's important to note that resource limits set using systemd are applied at the service level and do not affect other processes or services running on the system.


### Update the code-server service to limit its resource usage in Rocky Linux 8.8

## Executive summary

To limit the resources of the code-server service in Rocky Linux 8.8, you need to create a `.service` drop-in file in the `/etc/systemd/system/code-server.service.d/` directory. In this file, you can specify the resource limits using the `CPUQuota`, `MemoryLimit`, and `IOAccounting` directives. For example, to limit CPU usage to 50% and memory usage to 1GB, you can add the following lines:

```conf
[Service]
CPUQuota=50%
MemoryLimit=1G
```

After configuring the resource limits, you need to reload the systemd configuration and restart the service for the changes to take effect. Run the following commands:

```sh
sudo systemctl daemon-reload sudo systemctl restart code-server
```

The code-server service will now be limited to the specified resource limits. These limits are applied at the service level and do not affect other processes or services running on the system.

Here are the steps to follow in order to set CPU and Memory constraints on the code-server service running on Rocky Linux 8.8:

1. Create a directory to hold the service limits configuration:

```sh
sudo mkdir -p /etc/systemd/system/code-server@.service.d/
```

The `@` is important if the service runs under a user name. Replace code-server@ with code-server if your service doesn't run under a user.

2. Create a new configuration file in the newly created directory:

```sh
sudo nano /etc/systemd/system/code-server@.service.d/limits.conf
```

This will start the Nano text editor. You can use whichever editor you are comfortable with such as vi or emacs.

3. Insert the following contents into the file:

```conf
[Service]
CPUQuota=20%
MemoryLimit=500M
```

This configuration will limit the CPU usage of the service to 20% and the memory usage to 500MB. You can modify these settings depending on your needs.

4. Save the file and exit the editor. If you are using Nano, press CTRL-O to save and then CTRL-X to exit.

5. To have systemd pick up the new configuration, reload its configurations:

```sh
sudo systemctl daemon-reload
```

6. Finally, restart your service for the new limits to take effect immediately:

```sh
sudo systemctl restart code-server@
```

If your code-server does not run under a user, you should instead execute:

```sh
sudo systemctl restart code-server
```

With these steps, you have successfully placed CPU and Memory restrictions on your code-server service. These restrictions are specified in the `limits.conf` file and can be adjusted as needed.

For future reference, you can use similar techniques to set resource usage constraints on other services or processes in your Linux environment. This is generally accomplished through resource control directives in a `.service` file, or by using tools like `systemd-run`, `ulimit`, and `cpulimit`.
