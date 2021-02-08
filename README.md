# Ansible Role: Security

[![CI](https://github.com/libert-xyz/ansible-role-security/workflows/CI/badge.svg?event=push)](https://github.com/libert-xyz/ansible-role-security/actions?query=workflow%3ACI)


This is a fork from the Ansible role https://github.com/geerlingguy/ansible-role-security

Features added from the original role:

  - Install EPEL repo for RedHat based distributions
  - Add support for AmazonLinux 2
  - Add support for Ubuntu 20 LTS
  - Update / Upgrate security packages
  - SELinux Permissive mode


Features removed from the original role:

  - Automatic updates
  - Sudoers passworded users
  - Sudoers passwordless users
  - Remove Support for Fedora and Debian

Your servers' security is *your* responsibility.


## Requirements

For obvious reasons, `sudo` must be installed if you want to manage the sudoers file with this role.


## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    security_ssh_port: 2222

The port through which you'd like SSH to be accessible.

    security_ssh_password_authentication: "no"
    security_ssh_permit_root_login: "no"
    security_ssh_usedns: "no"
    security_ssh_permit_empty_password: "no"
    security_ssh_challenge_response_auth: "no"
    security_ssh_gss_api_authentication: "no"
    security_ssh_x11_forwarding: "no"

Security settings for SSH authentication. It's best to leave these set to `"no"`, but there are times (especially during initial server configuration or when you don't have key-based authentication in place) when one or all may be safely set to `'yes'`. **NOTE: It is _very_ important that you quote the 'yes' or 'no' values. Failure to do so may lock you out of your server.**

    security_sshd_state: started

The state of the SSH daemon. Typically this should remain `started`.

    security_ssh_restart_handler_state: restarted

The state of the `restart ssh` handler. Typically this should remain `restarted`.


    security_fail2ban_enabled: true

Whether to install/enable `fail2ban`. You might not want to use fail2ban if you're already using some other service for login and intrusion detection (e.g. [ConfigServer](http://configserver.com/cp/csf.html)).

    security_fail2ban_custom_configuration_template: "jail.local.j2"

The name of the template file used to generate `fail2ban`'s configuration.

## Dependencies

None.

## Example Playbook

    - hosts: servers
      become: true
      vars_files:
        - vars/main.yml
      roles:
        - libert_xyz.security

*Inside `vars/main.yml`*:

    security_fail2ban_enabled: False


## License

MIT

## Author Information

The original role was created in 2014 by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).

This role was updated by [Libert Schmidt](https://libert.xyz)