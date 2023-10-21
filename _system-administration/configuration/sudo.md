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
