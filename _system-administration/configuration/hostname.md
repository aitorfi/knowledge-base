---
layout: default
title: Hostname
parent: Configuration
---

# Hostname

Linux
{: .label .label-blue }

Networking
{: .label .label-yellow }

@see [man hostname](https://man7.org/linux/man-pages/man1/hostname.1.html), [hosts conf. file](../hosts)

The hostname is what a device is called on a network. To persistently change the hostname of your machine across reboots edit the file `/etc/hostname` or use the command `hostname new_host_name` to temporarily change it until the next reboot, you can also use the `hostname` command to check the current hostname. Once you've modified the hostname of your machine you might have to edit the `/etc/hosts` file specifying the new name.
