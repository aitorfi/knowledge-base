---
layout: default
title: Uncomplicated FireWall (UFW)
parent: Configuration
---

# Uncomplicated FireWall (UFW)

Linux
{: .label .label-blue }

@see [UFW wikipedia](https://en.wikipedia.org/wiki/Uncomplicated_Firewall), [UFW setup tutorial](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu-20-04) [UFW common rules and commands](https://www.digitalocean.com/community/tutorials/ufw-essentials-common-firewall-rules-and-commands)

The Uncomplicated Firewall (UFW) is a frontend for iptables and is particularly well-suited for host-based firewalls. UFW provides a framework for managing netfilter, as well as a command-line interface for manipulating the firewall. UFW aims to provide an easy to use interface for people unfamiliar with firewall concepts, while at the same time simplifies complicated iptables commands to help an administrator who knows what he or she is doing.

## Installation

UFW is available by default in all Ubuntu installations since 8.04 LTS and in all Debian installations since 10. However, UFW can be installed using the following command:

```bash
sudo apt install ufw
```

To check the status of UFW run the following command:

```bash
sudo ufw status
```

Run the following commands to enable and disable the firewall respectively:

```bash
sudo ufw enable
```

```bash
sudo ufw disable
```

## Configuration

The default configuration in UFW is to deny all incoming connections and allow all outgoing connections, to change this you use the following commands:

```bash
sudo ufw default deny incoming
```

```bash
sudo ufw default allow incoming
```

```bash
sudo ufw default allow outgoing
```

```bash
sudo ufw default deny outgoing
```

To allow connections to a service that runs in its default port and appears in the `/etc/services` file (for example ssh) run the following command:

```bash
sudo ufw allow ssh
```

If the service is not running in its default port or it does not appear in the `/etc/services` file you can enable connections to a specific port by running the following command:

```bash
sudo ufw allow [port]
```

To block incoming traffic on a specific port run the following command:

```bash
sudo ufw deny [port] 
```

To delete a rule use the following command:

```bash
sudo ufw delete [rule_number]
```

To find the number associated with a rule run the following command:

```bash
sudo ufw status numbered
```

To set a rate limit of incoming connections on a specific port (this might help prevent DoS attacks) run the following command:

```bash
sudo ufw limit [port]
```
