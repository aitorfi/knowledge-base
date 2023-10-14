# Mandatory Access Control (MAC)

@see [Wikipedia - MAC](https://en.wikipedia.org/wiki/Mandatory_access_control) [AppArmor site](https://apparmor.net/) [Wikipedia - SELinux](https://en.wikipedia.org/wiki/Security-Enhanced_Linux)

Mandatory Access Control (MAC) is a security mechanism implemented in Linux by some kernel modules like AppArmor and SELinux. MAC enforces strict access control on the system resources using policies that are applied to processes. By restricting access to resources a good behavior by those processes is ensured avoiding this way known and unknown security exploits.

## AppArmor vs SELinux

AppArmor is a kernel module focused on protecting individual applications and is known for being more user friendly than other MAC tools. Security-Enhanced Linux (SELinux) was originally developed by the United Stated National Security Agency (NSA) as a series of patches to the Linux kernel, it is known for being more robust and complex than other MAC tools.
