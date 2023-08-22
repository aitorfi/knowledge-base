---
layout: default
title: scp
parent: Tools
---

# scp

Linux
{: .label .label-blue }

Windows
{: .label .label-blue }

Networking
{: .label .label-yellow }

@see [man scp](https://man7.org/linux/man-pages/man1/scp.1.html), [ssh](../ssh)

**scp** copies files between hosts on a network. It uses ssh for data transfer, and uses the same authentication and provides the same security as a login session.

## Options

| Option  | Description                                                                          |
| ------- | ------------------------------------------------------------------------------------ |
| -P port | Specifies the port to connect to on the remote host.                                 |
| -p      | Preserves modification times, access times, and file mode bits from the source file. |
| -r      | Recursively copy entire directories.                                                 |

## Usage

Copy a file from a source host to a target host.

```bash
scp sourceuser@sourcehost:/source/path targetuser@targethost:/target/path
```

```bash
scp scp://sourceuser@sourcehost/source/path scp://targetuser@targethost:/target/path
```

Copy an entire directory from a source host to a target host.

```bash
scp -r sourceuser@sourcehost:/source/path targetuser@targethost:/target/path
```

```bash
scp -r scp://sourceuser@sourcehost/source/path scp://targetuser@targethost:/target/path
```

Copy a file from a source host to a target host specifying the port on the remote host, by default 22 (ssh default port).

```bash
scp -P 22000 sourceuser@sourcehost:/source/path targetuser@targethost:/target/path
```

```bash
scp scp://sourceuser@sourcehost:22000/path scp://targetuser@targethost:/target/path
```
