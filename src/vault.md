---
title: Install Vault
label: Install Vault
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


Vault stores, controls, and protects the data used for authentication and authorization. Vault is a management system for secrets, restricting or approving access to passwords, certificates, or APIs. It also provides data encryption, on-demand secrets, and revocation.

## Install `yum-config-manager`

```shell
sudo yum install -y yum-utils
```

## Add the HashiCorp Repo

```shell
sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/RHEL/hashicorp.repo
```

## Install

```shell
sudo yum -y install vault
```

## Verifying the Installation

```shell
vault

# Output
Usage: vault <command> [args]

Common commands:
    read        Read data and retrieves secrets
    write       Write data, configuration, and secrets
    delete      Delete secrets and configuration
    list        List data or secrets
    login       Authenticate locally
    agent       Start a Vault agent
    server      Start a Vault server
    status      Print seal and HA status
    unwrap      Unwrap a wrapped secret

Other commands:
    audit          Interact with audit devices
    auth           Interact with auth methods
    debug          Runs the debug command
    kv             Interact with Vault's Key-Value storage
    lease          Interact with leases
    monitor        Stream log messages from a Vault server
    namespace      Interact with namespaces
    operator       Perform operator-specific tasks
    path-help      Retrieve API help for paths
    plugin         Interact with Vault plugins and catalog
    policy         Interact with policies
    print          Prints runtime configurations
    secrets        Interact with secrets engines
    ssh            Initiate an SSH session
    token          Interact with tokens
```

## Run Vault as a Service

To run Vault as a service, you also need to create a new Systemd service file

```shell
sudo nano /etc/systemd/system/vault.service
```

Then, add the content below:

```conf
[Unit]
Description="HashiCorp Vault - A tool for managing secrets"
Documentation=https://www.vaultproject.io/docs/
Requires=network-online.target
After=network-online.target
ConditionFileNotEmpty=/etc/vault.d/vault.hcl
StartLimitIntervalSec=60
StartLimitBurst=3

[Service]
User=vault
Group=vault
ProtectSystem=full
ProtectHome=read-only
PrivateTmp=yes
PrivateDevices=yes
SecureBits=keep-caps
AmbientCapabilities=CAP_IPC_LOCK
Capabilities=CAP_IPC_LOCK+ep
CapabilityBoundingSet=CAP_SYSLOG CAP_IPC_LOCK
NoNewPrivileges=yes
ExecStart=/usr/local/bin/vault server -config=/etc/vault.d/vault.hcl
ExecReload=/bin/kill --signal HUP $MAINPID
KillMode=process
KillSignal=SIGINT
Restart=on-failure
RestartSec=5
TimeoutStopSec=30
StartLimitInterval=60
StartLimitIntervalSec=60
StartLimitBurst=3
LimitNOFILE=65536
LimitMEMLOCK=infinity

[Install]
WantedBy=multi-user.target
```

Enable and start the service with the commands:

```shell
sudo systemctl enable vault.service
```

```shell
sudo systemctl start vault.service
```

## Prepare to Administer Vault

The next step is to move the `Vault` bin directory to the `PATH` environment variable with the command:

```shell
export PATH=$PATH:/opt/vault/bin
echo "export PATH=$PATH:/opt/vault/bin" >> ~/.bashrc
```

Followed by setting the environment variables for Vault by typing:

```shell
export VAULT_ADDRESS=104.192.7.185:8200
echo "export VAULT_ADDR=104.192.7.185:8200" >> ~/.bashrc
```

## Initialize and Unseal your Vault

To initialize and unseal Vault, you will first need to start Vault as a server in the dev mode. However, make sure not to run a dev server in production.

Run the following command:

```shell
vault server -dev
```

The command produces an output that includes the server configuration, the unseal key, and root token. Save the unseal key and root token values, as you will need them in the next steps.

> **Note**: As Vault does not fork, you need to open another shell or terminal to run the following commands.

Start by setting the environment variable. You will find this command as part of the output from the previous steps:

```shell
export VAULT_ADDR=’http://127.0.0.1:8200’
```

Then, run the following command with the information from the dev server’s output:

````shell
export VAULT_DEV_ROOT_TOKEN_ID=”XXXXXXXXXXXXXXXX”
````

Check the status of the server:

```shell
vault status
```

The output should display that Vault is now initialized and no longer sealed.

```shell
Key             Value
---             -----
Seal Type       shamir
Initialized     true
Sealed          false
Total Shares    1
Threshold       1
Version         1.2.3
Cluster Name    vault-cluster-18e6bce0
Cluster ID      16382125-eb14-f23a-8145-ad64eee072cf
HA Enabled      false
```
