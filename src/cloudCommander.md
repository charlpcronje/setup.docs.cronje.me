---
title: Install Cloud Commander
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


Cloud Commander is a file manager for the web. It includes a command-line console and a text editor. Cloud Commander helps you manage your server and work with files, directories and programs in a web browser from any computer, mobile or tablet.

## Installation

Installation is very simple:

Install the latest version of node.js.
Install `cloudcmd` via npm with:

```shell
npm i cloudcmd -g
```

When in trouble, use:

```shell
npm i cloudcmd -g --force
```

## Cloud Commander as a Service

Not an issue actually, just want to share how I was able to add cloudcmd on systemd to start at boot especially for newbies like me since I was not able to find a guide on how to do it

```shell
sudo nano /etc/systemd/system/cloudcmd.service
```

Don't forget to change YOUR_USER_HERE with your actual user

```conf
[Unit]
Description=Cloud Commander

[Service]
TimeoutStartSec=0
User=YOUR_USER_HERE
Restart=always
ExecStart=/usr/bin/cloudcmd

[Install]
WantedBy=multi-user.target
```

once done, run the below commands to start and enable cloudcmd on boot

```shell
sudo systemctl enable --now cloudcmd
sudo systemctl status cloudcmd
```

now open your browser to url: [http://localhost:8000/](http://localhost:8000/)

## Usage

To start the server, just run the global npm binary from your terminal:

```shell
cloudcmd
```

Cloud Commander supports the following command-line parameters:

```conf
# Parameter Operation
-h, --help                    display help and exit
-v, --version                 display version and exit
-s, --save                    save configuration
-o, --online                  load scripts from remote servers
-a, --auth                    enable authorization
-u, --username                set username
-p, --password                set password
-c, --config                  configuration file path
--show-config                 show config values
--show-file-name              show file name in view and edit
--editor                      set editor: “dword”, “edward” or “deepword”
--packer                      set packer: “tar” or “zip”
--root                        set root directory
--prefix                      set url prefix
--prefix-socket               set prefix for url connection
--port                        set port number
--confirm-copy                confirm copy
--confirm-move                confirm move
--open                        open web browser when server starts
--name                        set tab name in web browser
--one-file-panel              show one file panel
--keys-panel                  show keys panel
--contact                     enable contact
--config-dialog               enable config dialog
--config-auth                 enable auth change in config dialog
--console                     enable console
--sync-console-path           sync console path
--terminal                    enable terminal
--terminal-path               set terminal path
--terminal-command            set command to run in terminal (shell by default)
--terminal-auto-restart       restart command on exit
--vim                         enable vim hot keys
--columns                     set visible columns
--export                      enable export of config through a server
--export-token                authorization token used by export server
--import                      enable import of config
--import-token                authorization token used to connect to export server
--import-url                  url of an import server
--import-listen               enable listen on config updates from import server
--dropbox                     enable dropbox integration
--dropbox-token               set dropbox token
--log                         enable logging
--no-show-config              do not show config values
--no-server                   do not start server
--no-auth                     disable authorization
--no-online                   load scripts from local server
--no-open                     do not open web browser when server started
--no-name                     set default tab name in web browser
--no-keys-panel               hide keys panel
--no-one-file-panel           show two file panels
--no-confirm-copy             do not confirm copy
--no-confirm-move             do not confirm move
--no-config-dialog            disable config dialog
--no-config-auth              disable auth change in config dialog
--no-console                  disable console
--no-sync-console-path        do not sync console path
--no-contact                  disable contact
--no-terminal                 disable terminal
--no-terminal-command         set default shell to run in terminal
--no-terminal-auto-restart    do not restart command on exit
--no-vim                      disable vim hot keys
--no-columns                  set default visible columns
--no-export                   disable export config through a server
--no-import                   disable import of config
--no-import-listen            disable listen on config updates from import server
--no-show-file-name           do not show file name in view and edit
--no-dropbox                  disable dropbox integration
--no-dropbox-token            unset dropbox token
--no-log                      disable logging
```

For options not specified by command-line parameters, Cloud Commander then reads configuration data from `~/.cloudcmd.json`. It uses port 8000 by default.

To begin using the web client, go to this URL in your browser:

```shell
http://localhost:8000
```

## Updating the app

If you installed Cloud Commander with npm, stop the server. Then, reinstall it with:

```shell
npm install cloudcmd -g
```

Then, start the server again with cloudcmd and reload the page.

## Hot keys

`Key`              `Operation`

```conf
F1                 help
F2                 show user menu
F3                 view, change directory
Shift + F3         view raw file, change directory
F4                 edit
F5                 copy
Alt + F5           pack
F6                 rename/move
Shift + F6         rename current file
F7                 new directory
Shift + F7         new file
F8, Delete         remove
Shift + Delete     remove without prompt
F9                 menu
Alt + F9           extract
F10                config
*                  select/unselect all
+                  expand selection
-                  shrink selection
Ctrl + X           cut to buffer
Ctrl + C           copy to buffer
Ctrl + V           paste from buffer
Ctrl + Z           clear buffer
Ctrl + P           copy path
Ctrl + R           refresh
Ctrl + D           clear local storage
Ctrl + A           select all files in a panel
Ctrl + M           rename selected files in editor
Ctrl + U           swap panels
Ctrl + F3          sort by name
Ctrl + F5          sort by date
Ctrl + F6          sort by size
Up, Down           file system navigation
Enter              change directory/view file
Alt + Left/Right   show content of directory under cursor in target panel
Alt + G            go to directory
Ctrl + \           go to the root directory
```

## Tab move via panels

Page Up             up on one page
Page Down           down on one page
Home                to begin of list
End                 to end of list
Space               select current file (and get size of directory)
Insert              select current file (and move to next)
F9                  context menu
~                   console

Esc toggle vim hotkeys (file manager, editor)

## Vim

When the `--vim` option is provided, or the configuration parameter `vim` is set, the following hotkeys become available:

| `Key`    | `Operation`                          |
|----------|--------------------------------------|
| j        | navigate to next file                |  
| k        | navigate to previous file            |
| dd       | remove current file                  |  
| G or $   | navigate to bottom file              |
| gg or ^  | navigate to top file                 |
| v        | visual mode                          |
| y        | copy (selected in visual mode files) |
| p        | paste files                          |
| Esc      | unselect all                         |
| /        | find file in current directory       |
| n        | navigate to next found file          |
| N        | navigate to previous found file      |

### Commands can be joined, for example

```conf
5j         will navigate 5 files below current;
d5j        will remove next 5 files;
dG         will remove all files from current to bottom;
```

### Drag and drop

These file operations are accessible with “drag and drop”.

```conf
Drag Mouse Button   Key     Origin     Destination        Operation
Left                        Panel      Panel              copy files
Left                Shift   Panel      Panel              rename/move files
Left                        Panel      Desktop            download files
Left                        Desktop   Panel               upload files
```

## View

![avator](https://cloudcmd.io/img/screen/view.png)

## Features

- View images.
- View text files.
- Play audio.
- Play video.

### Hotkeys (Features)

`Key`    `Operation`

```conf
F3      open
Esc    close
```

## Edit

![Edit](https://cloudcmd.io/img/screen/edit.png)

### Hot keys (Edit)

`Key`        `Operation`

```conf
F4          open
Shift + F4  open in “vim” mode
Esc         close
```

For more info visit the [official website](https://cloudcmd.io/#usage)
