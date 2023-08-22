---
layout: default
title: Hosts
parent: Configuration
---

# Hosts

@see [man hosts](https://man7.org/linux/man-pages/man5/hosts.5.html)

The hosts configuration file associates IP addresses with hostnames allowing you to access a device using these hostnames from a terminal or a web browser for example.

Host names may contain only alphanumeric characters, minus signs ("-"), and periods ("."). They must begin with an alphabetic character and end with an alphanumeric character. Optional aliases provide for name changes, alternate spellings, shorter hostnames, or generic hostnames (for example, _localhost_).

## File location by OS

| Operating System | File Path                             |
|------------------|---------------------------------------|
| Ubuntu           | /etc/hosts                            |
| Windows          | C:\\windows\\system32\\drivers\\etc\\hosts |


## Examples

### Ubuntu

```
# The following lines are desirable for IPv4 capable hosts
127.0.0.1       localhost

192.168.1.10    foo.mydomain.org       foo
192.168.1.13    bar.mydomain.org       bar
146.82.138.7    master.debian.org      master
209.237.226.90  www.opensource.org

# The following lines are desirable for IPv6 capable hosts
::1             localhost ip6-localhost ip6-loopback
ff02::1         ip6-allnodes
ff02::2         ip6-allrouters
```

### Windows

```
# Copyright (c) 1993-2006 Microsoft Corp.
#	
# This is a sample HOSTS file used by Microsoft TCP/IP for Windows.
#
# This file contains the mappings of IP addresses to host names. Each
# entry should be kept on an individual line. The IP address should
# be placed in the first column followed by the corresponding host name.
# The IP address and the host name should be separated by at least one
# space.
#
# Additionally, comments (such as these) may be inserted on individual
# lines or following the machine name denoted by a '#' symbol.
#
# For example:
#
#    102.54.94.97  rhino.acme.com   # source server
#    38.25.63.10   x.acme.com       # x client host

127.0.0.1 localhost
::1 localhost
```
