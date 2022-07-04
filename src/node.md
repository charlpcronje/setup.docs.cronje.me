---
title: Install Node.js 16 on CentOS 8 | CentOS 7
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


`Node.js` packages are provided through the NodeSource Node.js Binary Distributions via `.rpm`. Add the repository to the system using the commands below:

```shell
curl -fsSL https://rpm.nodesource.com/setup_16.x | sudo bash -
```

Once the repository has been configured on your CentOS server you can proceed to install Node.js 16 on CentOS 8 | CentOS 7:

```shell
sudo yum install -y nodejs
```

Confirm that you can start node shell:

```shell
node
```

Welcome to `Node.js v16.4.1`.
Type ".help" for more information.
> .exit
If you need development tools to build native addons:

```shell
sudo yum install gcc-c++ make
```

To install the Yarn package manager run the following commands:

```shell
curl -sL https://dl.yarnpkg.com/rpm/yarn.repo | sudo tee /etc/yum.repos.d/yarn.repo
sudo yum install yarn
```

Testing `Node.js 16` installation on CentOS 8 | CentOS 7

Once we have installed Node.js, let’s build our first web server. Create a file named app.js containing the following contents:

```shell
tee app.js<<EOL
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
EOL
```

Then run your web server using the following command

```shell
node app.js
```

This runs the service on port 3000

```shell
sudo ss -tuenlp | grep 3000

tcp     LISTEN   0        128            127.0.0.1:3000          0.0.0.0:*       users:(("node",pid=13377,fd=18)) ino:50295 sk:7 <->
```

 Visit [http://localhost:3000](http://localhost:3000) and you will see a message saying “Hello World“

## Upgrade Node.js

```shell
sudo yum remove -y nodejs npm
```

```shell
Removed:
  nodejs.x86_64 1:6.17.1-1.el7                                   npm.x86_64 1:3.10.10-1.6.17.1.1.el7
```

Complete!

Now let’s install the new version of Node.js:

```shell
sudo yum list available nodejs
```

Loaded plugins: `fastestmirror`, `langpacks`
Loading mirror speeds from cached hostfile

## Available Packages

nodejs.x86_64 2:12.14.1-1nodesource nodesource

```shell
sudo yum install nodejs
```
