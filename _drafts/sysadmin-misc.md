# Hostname

To change the hostname edit the file `/etc/hostname` or use the command `hostname`.

# Users

To create a new user you can use the low level utility `useradd` or the more user-friendly utility `adduser` which is basically a frontend for `useradd`. When using `adduser` you will be prompted to enter some information about the new user (only the password in mandatory).

```bash
adduser username
```

Similarly to adding a user, to delete one you can use the low level utility `userdel` or the more user-friendly `deluser` utility which is basically a frontend for `userdel`.

```bash
deluser username
```

When using `deluser` you have access to the following flags flags:

- **--remove-home:** Removes the home directory of the specified user.
- **--remove-all-files:** Removes all the files belonging to the specified user including its home directory.

To set a user's password as expired an thus forcing the user to change it on next loging run the dollowing command:

```bash
passwd --expire
```

or

```bash
passwd -e
```

# User group

To create a group run the following command:

```bash
groupadd group
```

To add a user to a group run the following command:

```bash
usermod -aG group user
```
