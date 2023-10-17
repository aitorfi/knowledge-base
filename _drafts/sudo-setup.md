# sudo Setup

## Installation

To install sudo run the following command:

```bash
apt-get install sudo
```

A user must be in the sudo group to be able to use the sudo command. To add a user to a group run the following command:

```bash
usermod -aG group user
```

## Configuration

The configuration file for sudo is `/etc/sudoers`. It is extremely important to always edit this file using `visudo` as it will check for syntax errors before writing the changes you made to the sudoers file.

{: .info }
> Visudo uses the default text editor. To change the editor for visudo run the command `sudo update-alternatives --config editor` and you will be prompted to choose an editor.

Following there is a listing of interesting configuration options for sudo:

- **passwd_tries:** Sets a maximum number of attempts to enter th password. Add the following line to the /etc/sudoers file to set a maximum of 3 attempts `Defaults passwd_tries=3`.
- **badpass_message:** Sets a custom message when a bad password is entered for the sudo command. Add the following line to the /etc/sudoers file to set this option `Defaults badpass_message="Custom error message for bad password"`.
- **requiretty:** Makes it mandatory to be logged into a tty to use sudo. Add the following line to the /etc/sudoers file to set this option `Defaults requiretty`.
