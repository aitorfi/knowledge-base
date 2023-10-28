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

## Paswword policies

@see [Some useful password policies](https://ostechnix.com/how-to-set-password-policies-in-linux/), [Debian libpam-pwquality man](https://manpages.debian.org/testing/libpam-pwquality/pam_pwquality.8.en.html)

It is a good practice to set a peridic expiration policy for user password to do this you can use the following options of the `/etc/login.defs` configuration file:

```
#
# Password aging controls:
#
#	PASS_MAX_DAYS	Maximum number of days a password may be used.
#	PASS_MIN_DAYS	Minimum number of days allowed between password changes.
#	PASS_WARN_AGE	Number of days warning given before a password expires.
#
PASS_MAX_DAYS	30
PASS_MIN_DAYS	2
PASS_WARN_AGE	7
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
