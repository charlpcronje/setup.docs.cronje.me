---
title: Set SSH Port
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>

I did npt believe this to be a big issue but every time I login to my server I get a message like this:

There were 46 failed login attempts since the last successful login.
Last login: Thu Jan 20 01:15:50 2022 from 197.89.36.53

And this was in the time span of 15min, so just to be safe, I am rather changing the port number:

## How SSH port on CentOS 7

**Step 1:** First, open `/etc/ssh/sshd_config` and search for the following Port 229 and make sure to choose an `unused/not-well-known` port (at least >1023).

**Step 2:** To open a port on firewallD, use the following command:

```shell
firewall-cmd --add-port YOUR_PORT_HERE/tcp
```

## SELinux Configuration

Configure SELinux to behave with the new port by typing the following command:

```shell
semanage port -a -t ssh_port_t -p tcp YOUR_PORT_HERE
```

## Fail2Ban Settings

**Step 1:** Open `/etc/fail2ban/jail.conf` and search for the following section to configure Fail2Ban:

```conf
[sshd]
# To use more aggressive sshd filter (inclusive sshd-ddos failregex)
#filter = sshd-aggressive

port = ssh

logpath = %(sshd_log)s

backend = %(sshd_backend)s
```

**Step 2:** Now, change the values of the port to the actual port by using the following commands. This example shows port 7222:

```conf
[sshd]
#To use a more aggressive sshd filter (inclusive sshd-ddos failregex):
#filter = sshd-aggressive

port = 7222
logpath = %(sshd_log)s
backend = %(sshd_backend)s
```

After the execution of these commands, Fail2Ban will not be able to close the appropriate port.

**Step 3:** Now, type the following commands to test the new configurations:

```shell
systemctl restart sshd
systemctl restart fail2ban
```

You can also try to connect via SSH to the server with the new port:

```sh
ssh USERNAME@YOUR_IP/HOSTNAME -p YOUR_NEW_PORT
```

Once you complete the aforementioned steps successfully, finalize the settings and mop up, meaning use the new port rather than the previous one.

**Step 4**: Configure the SSH daemon, open /etc/ssh/sshd_config delete/comment out the Port 22 in it.

Now you have told SSHD not to listen on port 22, which is the default port.

**Step 5**: It is time to finalize the firewall configuration:

```sh
firewall-cmd --add-port YOUR_PORT_HERE/tcp --permanent

firewall-cmd --reload

Step 6: After that, type the following commands:

systemctl restart sshd.service

firewall-cmd --remove-service ssh --permanent

firewall-cmd --reload
```

If you face the following  error when restarting the SSHD:

job for sshd.service failed because the control process exited with error code. See "systemctl status sshd.service" and `"journalctl -xe"` for details.

Run journalctl –xe by the command:

```sh
journalctl –xe
```

Upon execution of the command you will get an output like this:

```sh
server1 kernel: type=1400 audit(1537086072.510:4): avc: denied { name_bind } for pid=1074 comm="sshd" src=6378 scontext=system_u:system_r:sshd_t:s0-s0:c0.c1023 tcontext=system_u:object_r:unres

server1 sshd[1074]: error: Bind to port 6378 on 0.0.0.0 failed: Permission denied.

server1 sshd[1074]: error: Bind to port 6378 on :: failed: Permission denied.

server1 kernel: type=1400 audit(1537086072.515:5): avc: denied { name_bind } for pid=1074 comm="sshd" src=6378 scontext=system_u:system_r:sshd_t:s0-s0:c0.c1023 tcontext=system_u:object_r:unres

server1 sshd[1074]: fatal: Cannot bind any address.

server1 systemd[1]: sshd.service: main process exited, code=exited, status=255/n/a

server1 systemd[1]: Failed to start OpenSSH server daemon.
```

**Step 6**: You have to run the following commands to set the changes for the system:

`semanage port -a -t ssh_port_t -p tcp 3456``

**Step 7**: Now, you can verify that SELinux has allowed SSHD to listen on the two ports:

```sh
semanage port -l | grep ssh

ssh_port_t  tcp     3456, 22
```

**Step 8**: Next, type this command:

yum whatprovides semanage

The output should look like this:

```sh
policycoreutils-python-2.5-22.el7.x86_64 : SELinux policy core python utilities

Repo : base

Matched from:

Filename : /usr/sbin/semanage

Step 9: Now, install policycoreutils.

yum install -y policycoreutils-python

Step 10: Finally, check that you can log in to a server through a new SSH port with the following command:

ssh -p 3456 root@server1
```
