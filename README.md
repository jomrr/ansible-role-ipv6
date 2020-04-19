# ansible-role-ipv6

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

# Disable IPv6 via sysctl by default.
# This only results to no IPv6 addresses being assigned to any interface.
# The kernel module is still active, if this is your os default.
ipv6_disable_sysctl: True

# List of interfaces which should be configured via sysctl.
# This enables you to disable IPv6 on specified interfaces only.
# If empty (default), then all interfaces in ansible_interfaces
# plus 'all', 'default' and 'lo' are used, otherwise only listed ones.
# NOTE: Only applies if ipv6_disable_grub and ipv6_disable_kernel are False.
ipv6_only_interfaces: []

# Disable IPv6 via kernel parameter in the grub command line
ipv6_disable_grub: False

# Blacklist the IPv6 kernel module the ipv6 kernel module, if not built-in.
# NOTE: This setting is ignored when ipv6 module is built-in to the kernel.
#       This is the fact with most modern os verisons.
#       So you can leave it on safely to disable RedHat ifcfg settings for IPv6.
ipv6_disable_module: True
```

## Dependencies

None.

## Example Playbook

```yaml
---
# role: ansible-role-ipv6
# file: site.yml

- hosts: ipv6_systems
  become: True
  vars:
    ipv6_role_enabled: True
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
