---
title: Install Node Version Manager
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


`nvm` allows you to quickly install and use different versions of node via the command line.

**Example:**

```sh
$ nvm use 16
Now using node v16.9.1 (npm v7.21.1)
$ node -v
v16.9.1
$ nvm use 14
Now using node v14.18.0 (npm v6.14.15)
$ node -v
v14.18.0
$ nvm install 12
Now using node v12.22.6 (npm v6.14.5)
$ node -v
v12.22.6
```

## Install & Update Script

To **install** or **update** nvm, you should run the [install script][2]. To do that, you may either download and run the script manually, or use the following cURL or Wget command:

```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```

```sh
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```

Running either of the above commands downloads a script and runs it. The script clones the nvm repository to `~/.nvm`, and attempts to add the source lines from the snippet below to the correct profile file (`~/.bash_profile`, `~/.zshrc`, `~/.profile`, or `~/.bashrc`).

```sh
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

## Additional Notes

- If the environment variable `$XDG_CONFIG_HOME` is present, it will place the `nvm` files there.</sub>

- You can add `--no-use` to the end of the above script (...`nvm.sh --no-use`) to postpone using `nvm` until you manually [`use`](#usage) it.

- You can customize the install source, directory, profile, and version using the `NVM_SOURCE`, `NVM_DIR`, `PROFILE`, and `NODE_VERSION` variables.
Eg: `curl ... | NVM_DIR="path/to/nvm"`. Ensure that the `NVM_DIR` does not contain a trailing slash.

- The installer can use `git`, `curl`, or `wget` to download `nvm`, whichever is available.

## Troubleshooting on Linux

On Linux, after running the install script, if you get `nvm: command not found` or see no feedback from your terminal after you type `command -v nvm`, simply close your current terminal, open a new terminal, and try verifying again.
Alternatively, you can run the following commands for the different shells on the command line:

```sh
*bash*: `source ~/.bashrc`

*zsh*: `source ~/.zshrc`

*ksh*: `. ~/.profile`
```

These should pick up the `nvm` command.

## Verify Installation

To verify that nvm has been installed, do:

```sh
command -v nvm
```

which should output `nvm` if the installation was successful. Please note that `which nvm` will not work, since `nvm` is a sourced shell function, not an executable binary.

**Note:** On Linux, after running the install script, if you get `nvm: command not found` or see no feedback from your terminal after you type `command -v nvm`, simply close your current terminal, open a new terminal, and try verifying again.

### Important Notes

If you're running a system without prepackaged binary available, which means you're going to install nodejs or io.js from its source code, you need to make sure your system has a C++ compiler. For OS X, Xcode will work, for Debian/Ubuntu based GNU/Linux, the `build-essential` and `libssl-dev` packages work.

**Note:** `nvm` also support Windows in some cases. It should work through WSL (Windows Subsystem for Linux) depending on the version of WSL. It should also work with [GitBash](https://gitforwindows.org/) (MSYS) or [Cygwin](https://cygwin.com). Otherwise, for Windows, a few alternatives exist, which are neither supported nor developed by us:

- [nvm-windows](https://github.com/coreybutler/nvm-windows)
- [nodist](https://github.com/marcelklehr/nodist)
- [nvs](https://github.com/jasongin/nvs)

**Note:** `nvm` does not support [Fish] either (see [#303](https://github.com/nvm-sh/nvm/issues/303)). Alternatives exist, which are neither supported nor developed by us:

- [bass](https://github.com/edc/bass) allows you to use utilities written for Bash in fish shell
- [fast-nvm-fish](https://github.com/brigand/fast-nvm-fish) only works with version numbers (not aliases) but doesn't significantly slow your shell startup
- [plugin-nvm](https://github.com/derekstavis/plugin-nvm) plugin for [Oh My Fish](https://github.com/oh-my-fish/oh-my-fish), which makes nvm and its completions available in fish shell
- [fnm](https://github.com/fisherman/fnm) - [fisherman](https://github.com/fisherman/fisherman)-based version manager for fish
- [fish-nvm](https://github.com/FabioAntunes/fish-nvm) - Wrapper around nvm for fish, delays sourcing nvm until it's actually used.

### Git Install

If you have `git` installed (requires git v1.7.10+):

1. clone this repo in the root of your user profile
    - `cd ~/` from anywhere then `git clone https://github.com/nvm-sh/nvm.git .nvm`
1. `cd ~/.nvm` and check out the latest version with `git checkout v0.39.1`
1. activate `nvm` by sourcing it from your shell: `. ./nvm.sh`

Now add these lines to your `~/.bashrc`, `~/.profile`, or `~/.zshrc` file to have it automatically sourced upon login:
(you may have to add to more than one of the above files)

```sh
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```

### Manual Install

For a fully manual install, execute the following lines to first clone the `nvm` repository into `$HOME/.nvm`, and then load `nvm`:

```sh
export NVM_DIR="$HOME/.nvm" && (
  git clone https://github.com/nvm-sh/nvm.git "$NVM_DIR"
  cd "$NVM_DIR"
  git checkout `git describe --abbrev=0 --tags --match "v[0-9]*" $(git rev-list --tags --max-count=1)`
) && \. "$NVM_DIR/nvm.sh"
```

Now add these lines to your `~/.bashrc`, `~/.profile`, or `~/.zshrc` file to have it automatically sourced upon login:
(you may have to add to more than one of the above files)

```sh
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```

### Manual Upgrade

For manual upgrade with `git` (requires git v1.7.10+):

1. change to the `$NVM_DIR`
1. pull down the latest changes
1. check out the latest version
1. activate the new version

```sh
(
  cd "$NVM_DIR"
  git fetch --tags origin
  git checkout `git describe --abbrev=0 --tags --match "v[0-9]*" $(git rev-list --tags --max-count=1)`
) && \. "$NVM_DIR/nvm.sh"
```

## Usage

To download, compile, and install the latest release of node, do this:

```sh
nvm install node # "node" is an alias for the latest version
```

To install a specific version of node:

```sh
nvm install 14.7.0 # or 16.3.0, 12.22.1, etc
```

The first version installed becomes the default. New shells will start with the default version of node (e.g., `nvm alias default`).

You can list available versions using `ls-remote`:

```sh
nvm ls-remote
```

And then in any new shell just use the installed version:

```sh
nvm use node
```

Or you can just run it:

```sh
nvm run node --version
```

Or, you can run any arbitrary command in a subshell with the desired version of node:

```sh
nvm exec 4.2 node --version
```

You can also get the path to the executable to where it was installed:

```sh
nvm which 12.22
```

In place of a version pointer like "14.7" or "16.3" or "12.22.1", you can use the following special default aliases with `nvm install`, `nvm use`, `nvm run`, `nvm exec`, `nvm which`, etc:

- `node`: this installs the latest version of [`node`](https://nodejs.org/en/)
- `iojs`: this installs the latest version of [`io.js`](https://iojs.org/en/)
- `stable`: this alias is deprecated, and only truly applies to `node` `v0.12` and earlier. Currently, this is an alias for `node`.
- `unstable`: this alias points to `node` `v0.11` - the last "unstable" node release, since post-1.0, all node versions are stable. (in SemVer, versions communicate breakage, not stability).

### Long-term Support

Node has a [schedule](https://github.com/nodejs/Release#release-schedule) for long-term support (LTS) You can reference LTS versions in aliases and `.nvmrc` files with the notation `lts/*` for the latest LTS, and `lts/argon` for LTS releases from the "argon" line, for example. In addition, the following commands support LTS arguments:

- `nvm install --lts` / `nvm install --lts=argon` / `nvm install 'lts/*'` / `nvm install lts/argon`
- `nvm uninstall --lts` / `nvm uninstall --lts=argon` / `nvm uninstall 'lts/*'` / `nvm uninstall lts/argon`
- `nvm use --lts` / `nvm use --lts=argon` / `nvm use 'lts/*'` / `nvm use lts/argon`
- `nvm exec --lts` / `nvm exec --lts=argon` / `nvm exec 'lts/*'` / `nvm exec lts/argon`
- `nvm run --lts` / `nvm run --lts=argon` / `nvm run 'lts/*'` / `nvm run lts/argon`
- `nvm ls-remote --lts` / `nvm ls-remote --lts=argon` `nvm ls-remote 'lts/*'` / `nvm ls-remote lts/argon`
- `nvm version-remote --lts` / `nvm version-remote --lts=argon` / `nvm version-remote 'lts/*'` / `nvm version-remote lts/argon`

Any time your local copy of `nvm` connects to [https://nodejs.org](https://nodejs.org), it will re-create the appropriate local aliases for all available LTS lines. These aliases (stored under `$NVM_DIR/alias/lts`), are managed by `nvm`, and you should not modify, remove, or create these files - expect your changes to be undone, and expect meddling with these files to cause bugs that will likely not be supported.

To get the latest LTS version of node and migrate your existing installed packages, use

```sh
nvm install 'lts/*' --reinstall-packages-from=current
```

### Migrating Global Packages While Installing

If you want to install a new version of Node.js and migrate npm packages from a previous version:

```sh
nvm install node --reinstall-packages-from=node
```

This will first use "nvm version node" to identify the current version you're migrating packages from. Then it resolves the new version to install from the remote server and installs it. Lastly, it runs "nvm reinstall-packages" to reinstall the npm packages from your prior version of Node to the new one.

You can also install and migrate npm packages from specific versions of Node like this:

```sh
nvm install 6 --reinstall-packages-from=5
nvm install v4.2 --reinstall-packages-from=iojs
```

Note that reinstalling packages _explicitly does not update the npm version_ — this is to ensure that npm isn't accidentally upgraded to a broken version for the new node version.

To update npm at the same time add the `--latest-npm` flag, like this:

```sh
nvm install 'lts/*' --reinstall-packages-from=default --latest-npm
```

or, you can at any time run the following command to get the latest supported npm version on the current node version:

```sh
nvm install-latest-npm
```

If you've already gotten an error to the effect of "npm does not support Node.js", you'll need to (1) revert to a previous node version (`nvm ls` & `nvm use <your latest _working_ version from the ls>`, (2) delete the newly created node version (`nvm uninstall <your _broken_ version of node from the ls>`), then (3) rerun your `nvm install` with the `--latest-npm` flag.

### Default Global Packages From File While Installing

If you have a list of default packages you want installed every time you install a new version, we support that too -- just add the package names, one per line, to the file `$NVM_DIR/default-packages`. You can add anything npm would accept as a package argument on the command line.

```sh
# $NVM_DIR/default-packages

rimraf
object-inspect@1.0.2
stevemao/left-pad
```

### io.js

If you want to install [io.js](https://github.com/iojs/io.js/):

```sh
nvm install iojs
```

If you want to install a new version of io.js and migrate npm packages from a previous version:

```sh
nvm install iojs --reinstall-packages-from=iojs
```

The same guidelines mentioned for migrating npm packages in node are applicable to io.js.

### System Version of Node

If you want to use the system-installed version of node, you can use the special default alias "system":

```sh
nvm use system
nvm run system --version
```

### Listing Versions

If you want to see what versions are installed:

```sh
nvm ls
```

If you want to see what versions are available to install:

```sh
nvm ls-remote
```

### Setting Custom Colors

You can set five colors that will be used to display version and alias information. These colors replace the default colors.

```conf
  Initial colors are: g b y r e

  Color codes:

    r/R = red / bold red

    g/G = green / bold green

    b/B = blue / bold blue

    c/C = cyan / bold cyan

    m/M = magenta / bold magenta

    y/Y = yellow / bold yellow

    k/K = black / bold black

    e/W = light grey / white
```

```sh
nvm set-colors rgBcm
```

#### Persisting custom colors

If you want the custom colors to persist after terminating the shell, export the NVM_COLORS variable in your shell profile. For example, if you want to use cyan, magenta, green, bold red and bold yellow, add the following line:

```sh
export NVM_COLORS='cmgRY'
```

#### Suppressing colorized output

`nvm help (or -h or --help)`, `nvm ls`, `nvm ls-remote` and `nvm alias` usually produce colorized output. You can disable colors with the `--no-colors` option (or by setting the environment variable `TERM=dumb`):

```sh
nvm ls --no-colors
nvm help --no-colors
TERM=dumb nvm ls
```

#### Restoring PATH

To restore your PATH, you can deactivate it:

```sh
nvm deactivate
```

#### Set default node version

To set a default Node version to be used in any new shell, use the alias 'default':

```sh
nvm alias default node
```

#### Use a mirror of node binaries

To use a mirror of the node binaries, set `$NVM_NODEJS_ORG_MIRROR`:

```sh
export NVM_NODEJS_ORG_MIRROR=https://nodejs.org/dist
nvm install node

NVM_NODEJS_ORG_MIRROR=https://nodejs.org/dist nvm install 4.2
```

To use a mirror of the io.js binaries, set `$NVM_IOJS_ORG_MIRROR`:

```sh
export NVM_IOJS_ORG_MIRROR=https://iojs.org/dist
nvm install iojs-v1.0.3

NVM_IOJS_ORG_MIRROR=https://iojs.org/dist nvm install iojs-v1.0.3
```

`nvm use` will not, by default, create a "current" symlink. Set `$NVM_SYMLINK_CURRENT` to "true" to enable this behavior, which is sometimes useful for IDEs. Note that using `nvm` in multiple shell tabs with this environment variable enabled can cause race conditions.

### .nvmrc

You can create a `.nvmrc` file containing a node version number (or any other string that `nvm` understands; see `nvm --help` for details) in the project root directory (or any parent directory).
Afterwards, `nvm use`, `nvm install`, `nvm exec`, `nvm run`, and `nvm which` will use the version specified in the `.nvmrc` file if no version is supplied on the command line.

For example, to make nvm default to the latest 5.9 release, the latest LTS version, or the latest node version for the current directory:

```sh
echo "5.9" > .nvmrc

echo "lts/*" > .nvmrc # to default to the latest LTS version

echo "node" > .nvmrc # to default to the latest version
```

[NB these examples assume a `POSIX`-compliant shell version of `echo`. If you use a Windows `cmd` development environment, eg the `.nvmrc` file is used to configure a remote Linux deployment, then keep in mind the `"`s will be copied leading to an invalid file. Remove them.]

Then when you run nvm:

```sh
nvm use
Found '/path/to/project/.nvmrc' with version <5.9>
Now using node v5.9.1 (npm v3.7.3)
```

`nvm use` et. al. will traverse directory structure upwards from the current directory looking for the `.nvmrc` file. In other words, running `nvm use` et. al. in any subdirectory of a directory with an `.nvmrc` will result in that `.nvmrc` being utilized.

The contents of a `.nvmrc` file **must** be the `<version>` (as described by `nvm --help`) followed by a newline. No trailing spaces are allowed, and the trailing newline is required.

### Deeper Shell Integration

You can use [`avn`](https://github.com/wbyoung/avn) to deeply integrate into your shell and automatically invoke `nvm` when changing directories. `avn` is **not** supported by the `nvm` maintainers. Please [report issues to the `avn` team](https://github.com/wbyoung/avn/issues/new).

If you prefer a lighter-weight solution, the recipes below have been contributed by `nvm` users. They are **not** supported by the `nvm` maintainers. We are, however, accepting pull requests for more examples.

#### bash

##### Automatically call `nvm use`

Put the following at the end of your `$HOME/.bashrc`:

```bash
cdnvm() {
    command cd "$@";
    nvm_path=$(nvm_find_up .nvmrc | tr -d '\n')

    # If there are no .nvmrc file, use the default nvm version
    if [[ ! $nvm_path = *[^[:space:]]* ]]; then

        declare default_version;
        default_version=$(nvm version default);

        # If there is no default version, set it to `node`
        # This will use the latest version on your machine
        if [[ $default_version == "N/A" ]]; then
            nvm alias default node;
            default_version=$(nvm version default);
        fi

        # If the current version is not the default version, set it to use the default version
        if [[ $(nvm current) != "$default_version" ]]; then
            nvm use default;
        fi

    elif [[ -s $nvm_path/.nvmrc && -r $nvm_path/.nvmrc ]]; then
        declare nvm_version
        nvm_version=$(<"$nvm_path"/.nvmrc)

        declare locally_resolved_nvm_version
        # `nvm ls` will check all locally-available versions
        # If there are multiple matching versions, take the latest one
        # Remove the `->` and `*` characters and spaces
        # `locally_resolved_nvm_version` will be `N/A` if no local versions are found
        locally_resolved_nvm_version=$(nvm ls --no-colors "$nvm_version" | tail -1 | tr -d '\->*' | tr -d '[:space:]')

        # If it is not already installed, install it
        # `nvm install` will implicitly use the newly-installed version
        if [[ "$locally_resolved_nvm_version" == "N/A" ]]; then
            nvm install "$nvm_version";
        elif [[ $(nvm current) != "$locally_resolved_nvm_version" ]]; then
            nvm use "$nvm_version";
        fi
    fi
}
alias cd='cdnvm'
cd "$PWD"
```

This alias would search 'up' from your current directory in order to detect a `.nvmrc` file. If it finds it, it will switch to that version; if not, it will use the default version.

#### zsh

##### Calling `nvm use` automatically in a directory with a `.nvmrc` file

Put this into your `$HOME/.zshrc` to call `nvm use` automatically whenever you enter a directory that contains an
`.nvmrc` file with a string telling nvm which node to `use`:

```zsh
# place this after nvm initialization!
autoload -U add-zsh-hook
load-nvmrc() {
  local node_version="$(nvm version)"
  local nvmrc_path="$(nvm_find_nvmrc)"

  if [ -n "$nvmrc_path" ]; then
    local nvmrc_node_version=$(nvm version "$(cat "${nvmrc_path}")")

    if [ "$nvmrc_node_version" = "N/A" ]; then
      nvm install
    elif [ "$nvmrc_node_version" != "$node_version" ]; then
      nvm use
    fi
  elif [ "$node_version" != "$(nvm version default)" ]; then
    echo "Reverting to nvm default version"
    nvm use default
  fi
}
add-zsh-hook chpwd load-nvmrc
load-nvmrc
```
