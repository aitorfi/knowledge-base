---
layout: default
title: Sudo
parent: Configuration
---

# Sudo

Linux
{: .label .label-blue }

@see [man sudo](https://man7.org/linux/man-pages/man8/sudo.8.html), [man sudoers](https://man7.org/linux/man-pages/man5/sudoers.5.html)

`sudo` (short for "superuser do") is a command that allows authorized users to execute commands with superuser privileges, typically as the root user, on Unix-like operating systems. It provides a way to delegate limited administrative powers to regular users while maintaining a log of their activities.

## Installation

To install sudo run the following command:

```bash
apt-get install sudo
```

A user must be in the sudo group to be able to use the sudo command. To add a user to the sudo group run the following command as root:

```bash
usermod -aG sudo user
```

## Usage

To use sudo, you need to have the necessary permissions. Generally, only the system administrator (root) can grant these permissions. To execute a command with superuser privileges simply add 'sudo' before the command:

```bash
sudo command
```

Note that when you run a command using sudo you will be prompted to enter your password.

## Configuration

The configuration file for sudo is `/etc/sudoers`, following there is a listing of interesting configuration options for sudo:

{: .warning }
It is extremely important to always edit `/etc/sudoers` using `visudo` command as it will check for syntax errors before writing the changes you made.

{: .info }
> Visudo uses the default text editor. To change the editor for visudo run the command `sudo update-alternatives --config editor` and you will be prompted to choose an editor.

- **passwd_tries:** Sets a maximum number of attempts to enter th password.
- **badpass_message:** Sets a custom message when a bad password is entered for the sudo command.
- **requiretty:** Makes it mandatory to be logged into a tty to use sudo, this prevents the use of sudo from daemons and other detached processes like cronjobs.
- **log_input:** A flag that instructs sudo to log the input of every command run with sudo.
- **log_output:** A flag that instructs sudo to log the output of every command run with sudo.
- **iolog_dir:** Specifies the directory where input/output logs will be stored.
- **secure_path:** The value specified with this option is used in place of the user's PATH environment varibale, basically it specifies the directories that can be used with sudo.

Here is an example of an /etc/sudoers file that uses these configuration options:

```
#
# This file MUST be edited with the 'visudo' command as root.
#
# Please consider adding local content in /etc/sudoers.d/ instead of
# directly modifying this file.
#
# See the man page for details on how to write a sudoers file.
#
Defaults	env_reset
Defaults	mail_badpass
Defaults	secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"

# This fixes CVE-2005-4890 and possibly breaks some versions of kdesu
# (#1011624, https://bugs.kde.org/show_bug.cgi?id=452532)
Defaults	use_pty

# This preserves proxy settings from user environments of root
# equivalent users (group sudo)
#Defaults:%sudo env_keep += "http_proxy https_proxy ftp_proxy all_proxy no_proxy"

# This allows running arbitrary commands, but so does ALL, and it means
# different sudoers have their choice of editor respected.
#Defaults:%sudo env_keep += "EDITOR"

# Completely harmless preservation of a user preference.
#Defaults:%sudo env_keep += "GREP_COLOR"

# While you shouldn't normally run git as root, you need to with etckeeper
#Defaults:%sudo env_keep += "GIT_AUTHOR_* GIT_COMMITTER_*"

# Per-user preferences; root won't have sensible values for them.
#Defaults:%sudo env_keep += "EMAIL DEBEMAIL DEBFULLNAME"

# "sudo scp" or "sudo rsync" should be able to use your SSH agent.
#Defaults:%sudo env_keep += "SSH_AGENT_PID SSH_AUTH_SOCK"

# Ditto for GPG agent
#Defaults:%sudo env_keep += "GPG_AGENT_INFO"

# BEGIN CUSTOM CONFIGURATION

# Set max attempts to enter password:
Defaults	passwd_tries=3
# Set custom message on bad password:
Defaults	badpass_message="No te sabes tu contraseña?"
# Specifies that a tty session is mandatory to use sudo:
Defaults	requiretty
# Specifies the directory to store i/o logs:
Defaults	iolog_dir="/var/log/sudo/"
# Turns on command input logging;
Defaults	log_input
# Turns on command output logging:
Defaults	log_output

# END CUSTOM CONFIGURATION

# Host alias specification

# User alias specification

# Cmnd alias specification

# User privilege specification
root	ALL=(ALL:ALL) ALL

# Allow members of group sudo to execute any command
%sudo	ALL=(ALL:ALL) ALL

# See sudoers(5) for more information on "@include" directives:

@includedir /etc/sudoers.d
```
