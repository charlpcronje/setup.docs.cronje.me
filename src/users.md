# Adding some users

- For me it is firstly important to obviously have a root user, with a good strong password.
- Then to have another user in the sudo group that will be my every day user
- Then I might add some more users for some actual users
- Some users for some specific packages

I already updated the `root` user's password to something else by using this command:

## Update root password

```shell
sudo passwd root

# Enter new password
*************
# Confirm new password
*************
```

## Verify the Wheel Group is Enabled

Update sudo to allow all commands

```shell
visudo
```

Scroll through the configuration file until you see the following entry:

```shell
## Allows people in group wheel to run all commands

# %wheel        ALL=(ALL)       ALL
```

If the second line begins with the # sign, it has been disabled and marked as a comment. Just delete the # sign at the beginning of the second line so it looks like the following:

```shell
%wheel        ALL=(ALL)       ALL
```

## Add new `sudo` user

Then I created a new user that I used my initials for, lets say `cc`

```shell
useradd cc
passwd cc

# Enter new password
*************
# Confirm new password
*************
```

## Add `cc` to `sudo` group

```shell
usermod –aG wheel `cc`
```

## Switch to the Sudo User

Switch to the new (or newly-elevated) user account with the su (substitute user) command:

```shell
su - cc
```

Enter the password if prompted. The terminal prompt should change to include the UserName.

Enter the following command to list the contents of the /root directory:

```shell
sudo ls -la /root
```

## Alternative: Add User to Sudoers Configuration File

If there’s a problem with the wheel group, or administrative policy prevents you from creating or modifying groups, you can add a user directly to the sudoers configuration file to grant sudo privileges.

### Step 1: Open the Sudoers File in an Editor

In the terminal, run the following command:

```shell
visudo
```

This will open the `/etc/sudoers` file in a text editor.

### Step 2: Add the New User to file

Scroll down to find the following section:

```shell
## Allow root to run any commands anywhere

root ALL=(ALL) ALL
```

Right after this entry, add the following text:

```shell
UserName ALL=(ALL) ALL
```

Replace `UserName` with the username you created in Step 2. This section should look like the following:

```shell
## Allow root to run any commands anywhere

root ALL=(ALL) ALL

UserName ALL=(ALL) ALL
```

Save the file and exit.

### Step 3: Test Sudo Privileges for the User Account

Switch user accounts with the su (substitute user) command:

```shell
su — UserName
```

Enter the password for the account, if prompted. The terminal prompt should change to include UserName.

List the contents of the `/root` directory:

```shell
sudo ls —la /root
```

Enter the password for this user when prompted. The terminal should display a list of all the directories in the `/root` directory.
