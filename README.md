# ansible-role-ipv6

![GitHub](https://img.shields.io/github/license/jam82/ansible-role-ipv6) [![Build Status](https://travis-ci.org/jam82/ansible-role-ipv6.svg?branch=master)](https://travis-ci.org/jam82/ansible-role-ipv6)

**Ansible role for enabling or disabling ipv6.**

## Supported Platforms

- Alpine 3.11
- Amazonlinux 2
- Archlinux
- CentOS 7, 8
- Debian 9, 10
- Fedora 31
- Oraclelinux 7, 8
- Suse 15
- Ubuntu 18.04, 20.04

## Requirements

Ansible 2.9 or higher is recommended.

## Variables

Variables and defaults for this role:

```yaml
---
# role: ansible-role-ipv6
# file: defaults/main.yml

# The role is disabled by default, so you do not get in trouble.
# Checked in tasks/main.yml which includes tasks.yml if enabled.
# The default pattern of {role_name}_enabled is unhandy here...
ipv6_role_enabled: False

# Disable IPv6 via kernel parameter in the grub command line
ipv6_disable_grub: False

# Reboot immediately after GRUB_CMDLINE_LINUX changed
ipv6_reboot_after_grub_change: False

# Blacklist the IPv6 kernel module the ipv6 kernel module, if not built-in
# and for os_family=RedHat set NETWORKING_IPV6 and IPV6INIT to "no".
# NOTE: This setting is ignored when ipv6 module is built-in to the kernel.
#       This is true for most modern operating systems, so you can leave it
#       enabled safely to disable RedHat ifcfg settings for IPv6.
ipv6_disable_module: True

# Disable IPv6 via sysctl by default.
# This only results to no IPv6 addresses being assigned to any interface.
# The kernel module is still active, if this is your os default.
# NOTE: When ipv6_disable_grub=true this has no effect.
ipv6_disable_sysctl: True
```

## Dependencies

- ansible-role-hosts (optional)

## Example Playbook

```yaml
---
# role: ansible-role-ipv6
# file: site.yml

- hosts: all
  become: True
  vars:
    ipv6_role_enabled: True
    ipv6_disable_grub: True
  roles:
    - role: ansible-role-ipv6
```

## License and Author

- Author:: [jam82](https://github.com/jam82/)
- Copyright:: 2020, [jam82](https://github.com/jam82/)

Licensed under [MIT License](https://opensource.org/licenses/MIT).
See [LICENSE](https://github.com/jam82/ansible-role-ipv6/blob/master/LICENSE) file in repository.

## References

- [ArchWiki - IPv6](https://wiki.archlinux.org/index.php/IPv6)
- [Gloaded Journal - How to Disable IPv6 in Fedora and CentOS](https://www.g-loaded.eu/2008/05/12/how-to-disable-ipv6-in-fedora-and-centos/)
