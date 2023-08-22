---
layout: default
title: Aliases
parent: Miscellaneous
---

# Aliases

Linux
{: .label .label-blue }

Tricks
{: .label .label-yellow }

@see [man alias](https://man7.org/linux/man-pages/man1/alias.1p.html), [man unalias](https://man7.org/linux/man-pages/man1/unalias.1p.html)

When we often have to use a single big command multiple times, in those cases, we create something called as **alias** for that command. An alias instructs the shell to replace one string with another string while executing the commands.

An alias can be set by using the command `alias` or it can be persisted by using the files `~/.bash_aliases` or `~/.bashrc`.

## *alias* command

The alias command is used to create or redefine aliases. It can also be used to write existing aliases to standard output. An alias definition affects the current shell execution environment and the execution environments of the subshells of the current shell.

### Usage

`alias [-p] [alias-name[=value] ... ]`

Create an alias for a commonly used `ls` command:

```bash
alias lf="ls -CF"
```

Write the definition of the `lf` alias to standard output:

```bash
alias lf
```

Write all the defined aliases to standard output:

```bash
alias

alias -p
```

## *unalias* command

The unalias command is used to remove the definition for each alias name specified. The aliases are removed from the current shell execution environment.

### Usage

`unalias alias-name...`

`unalias -a`

Remove the definition of all aliases:

```bash
unalias -a
```

Remove the definition of the `lf` alias:

```bash
unalias lf
```

## *bash_aliases* file

Aliases can be persisted in the file `~/.bash_aliases`. The content of the file is a series of calls the `alias` command that will be executed on system startup.

### Example

```
# Copies the standard input to the clipboard
# Usage: cat file | copy
alias copy='xsel -ib'

# Mount terminus-nas network share to /media/terminus
alias terminus='sudo mount -t cifs -o uid=1000,gid=1000,username=ubuntu //192.168.1.200/terminus-nas /media/terminus'

# Unmount terminus-nas network share from /media/terminus
alias uterminus='sudo umount /media/terminus'
```

## *bashrc* file

Aliases can be persisted in the `~/.bashrc` file the same way they are persisted in the `~/bash_aliases` file.
