# Uncomplicated FireWall (UFW)

@see [UFW wikipedia](https://en.wikipedia.org/wiki/Uncomplicated_Firewall), [UFW setup tutorial](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu-20-04) [UFW common rules and commands](https://www.digitalocean.com/community/tutorials/ufw-essentials-common-firewall-rules-and-commands)

The Uncomplicated Firewall (ufw) is a frontend for iptables and is particularly well-suited for host-based firewalls. ufw provides a framework for managing netfilter, as well as a command-line interface for manipulating the firewall. ufw aims to provide an easy to use interface for people unfamiliar with firewall concepts, while at the same time simplifies complicated iptables commands to help an administrator who knows what he or she is doing.

## Installation

UFW is available by default in all Ubuntu installations since 8.04 LTS and in all Debian installations since 10. However, UFW can be installed using the following command:

```bash
sudo apt install ufw
```

To check the status of UFW run the following command:

```bash
sudo ufw status
```

## Configurtion

The default consiguration in UFW is to deny all incoming connections and allow all outgoing connections, to change this you use the following commands:

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

To allow connections to a service that runs in the its default port and appears in the `/etc/services` file (for example ssh) run the following command:

```bash
sudo ufw allow ssh
```

If the service is not running in its default port or it does not appear in the `/etc/services` file you can enable connections to a specific port by running the following command:

```bash
sudo ufw allow 4242
```
