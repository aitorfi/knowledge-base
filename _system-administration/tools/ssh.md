---
layout: default
title: ssh
parent: Tools
---

# ssh

Linux
{: .label .label-blue }

Windows
{: .label .label-blue }

Networking
{: .label .label-yellow }

@see [man ssh](https://man7.org/linux/man-pages/man1/ssh.1.html)

**ssh** (SSH client) is a program for logging into a remote machine and for executing commands on a remote machine. It is intended to provide secure encrypted communications between two untrusted hosts over an insecure network.

## Usage

Basic usage of the command, you will be prompted to provide the password of the user.

```bash
ssh username@hostname
```

```bash
ssh username@192.168.1.200
```

Specify the ssh port on the remote host, by default is 22.

```bash
ssh username@hostname -p 22000
```
