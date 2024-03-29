---
title: Install Samba on CentOS 7
label: Install Samba on CentOS 7
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


The first thing we have to do is to install samba on our machine. The package and the needed libraries are available in the official `RHEL 7` / `CentOS 7` repositories, therefore we can install them just by using `yum` or `dnf`. In this version of `RHEL/CentOS`, the first command it’s just a `link` to the second:

```shell
sudo dnf install samba samba-common samba-client
```

The samba-client package is not strictly needed, but the utilities provided by it can be useful. Once the packages are installed, we have to start and enable the `smb` and the `nmb` daemons at boot. The first is the daemon which takes care of performing the actual transfers and the sharing operations, while the second performs the `NetBIOS` name resolutions, allowing the resources to appear when browsing the network on Windows. We can now enable and start both `systemd services` with just one command:

```shell
sudo systemctl enable --now {smb,nmb}
```

Normally you would need to configure the firewall but we disabled it so :)

## Configuring a shared directory accessible by guests

Let’s say we want to share a directory via samba, and we want to let free access to this directory to guest users, without them having to provide a password. To obtain the desired result, we must make some changes to the `/etc/samba/smb.conf` file, and add a “stanza” for our share. Open the file with your favorite editor, and in the `[`global]` section, add the highlighted text:

### Configuring  Samba

```shell
mv /etc/samba/smb.conf /etc/samba/smb.con.bak
```

I want to share /var/www, normally you would do the following to create a share

```shell
sudo mkdir -p /srv/samba/shared
sudo chmod -R 0755 /srv/samba/shared
sudo chown -R nobody:nobody /srv/samba/shared
sudo chcon -t samba_share_t /srv/samba/share
```

But in this case I already have the folders I want to share and I need to keep the ownership to apache,
so all I can do for now is

```shell
chcon -h system_u:object_r:bin_t:s0 /var/www
```

Now create a new samba configuration file

```shell
sudo nano /etc/samba/smb.conf
```

### Creating secure shares in Samba

The file share we just created is accessible to everyone and any user can create and delete files. This poses a challenge if you want to share critical documents  as they can be overwritten or deleted as well. For this reason, we need to create a secure file share to address this challenge.

First, we are going to create a new group for samba users as shown:

```shell
sudo groupadd secure_group
```

Then we shall add a new user to the newly created group

```shell
sudo useradd -g secure_group charl
```

necessary permissions and file ownership as shown below .

```shell
sudo chcon -t samba_share -p /var/www
sudo chown -R charl:secure_group /var/www
```

 This will prompt you to provide a SMP password and later confirm it.

```shell
 sudo smbpasswd -a charl
```

```shell
sudo nano /etc/samba/smb.conf
```

Append the config below

```conf
[global]
# Set the workgroup to the same as the network domain
workgroup = isa
# This will be the device name on the network
netbios name = CentOS-8
# This will let linux users access the share
security = user
# This sets the network to be discoverable by windows
wins support = yes

[Share]
# The path that will be shared
path = /var/www
# No matter who logged in he will be treated as if he is the apache user
force user = apache
writeable = yes
browseable = yes
# No matter who logged in he will be treated as if he is in the apache group
force group = apache
# All new files that is created will het this permissions
create mask = 0644
read only = no
guest ok = yes
# All new folders that is created will het this permissions
directory mask = 0755 
```

### Start and enable Samba services

```shell
sudo systemctl start smb
sudo systemctl enable smb
```

Then confirm if smb service is running:

```shell
sudo systemctl status smb
```

```shell
sudo systemctl start nmb
sudo systemctl enable nmb
```

Similarly confirm if nmb service is running just like we did with smb service:

```shell
sudo systemctl status nmb
```

I then connected the share as a network drive, In windows right click `This PC` and click on `Map network drive`

- path: `\\[server ip]\Share`
- Drive letter: S:

### Make apache group share

```shell
sudo groupadd apache
sudo useradd apache -G apache
# Change the group to apache
chgrp -R apache /var/www
# Change the owner to apache
chown -R apache /var/www
# replicate the group and permissions as they have been set
chmod g+s /var/www
```
