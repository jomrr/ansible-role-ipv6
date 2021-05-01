# ansible-role-ipv6

![GitHub](https://img.shields.io/github/license/jam82/ansible-role-ipv6) [![Build Status](https://travis-ci.org/jam82/ansible-role-ipv6.svg?branch=main)](https://travis-ci.org/jam82/ansible-role-ipv6)

**Ansible role for enabling or disabling IPv6 via sysctl.**

## Supported Platforms

- Alpine
- Amazonlinux
- Archlinux
- CentOS
- Debian
- Fedora
- Manjaro
- OracleLinux
- OpenSuse Leap, Tumbleweed
- Ubuntu

## Requirements

Ansible 2.9 or higher is recommended.

## Variables

Removed `GRUB`, `modprobe` and `ifcg-script` options for simplicity,
as IPv6 module is builtin in the most kernels by default.

Variables and defaults for this role:

```yaml
---
# role: ansible-role-ipv6
# file: defaults/main.yml

# The role is disabled by default, so you do not get in trouble.
# Checked in tasks/main.yml which includes tasks.yml if enabled.
ipv6_role_enabled: false

# Disable IPv6 via sysctl by default.
# This only results to no IPv6 addresses being assigned to any interface.
# The kernel module is still active, if this is your os default.
ipv6_disable_sysctl: true

# Configuration file for sysctl
ipv6_sysctl_file: "/etc/sysctl.d/98-ipv6.conf"
```

## Dependencies

- ansible-role-hosts (optional)

## Example Playbook

```yaml
---
# role: ansible-role-ipv6
# file: site.yml

- hosts: all
  become: true
  vars:
    ipv6_role_enabled: true
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
