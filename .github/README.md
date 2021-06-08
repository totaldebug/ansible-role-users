<h4 align="center">An Ansible role for creating users and groups.</h4>

<p align="center">
    <a href="https://github.com/totaldebug/ansible-role-users/commits/master">
    <img src="https://img.shields.io/github/last-commit/totaldebug/ansible-role-users.svg?style=flat-square&logo=github&logoColor=white"
         alt="GitHub last commit">
    <a href="https://github.com/totaldebug/ansible-role-users/issues">
    <img src="https://img.shields.io/github/issues-raw/totaldebug/ansible-role-users.svg?style=flat-square&logo=github&logoColor=white"
         alt="GitHub issues">
    <a href="https://github.com/totaldebug/ansible-role-users/pulls">
    <img src="https://img.shields.io/github/issues-pr-raw/totaldebug/ansible-role-users.svg?style=flat-square&logo=github&logoColor=white"
         alt="GitHub pull requests">
</p>

<p align="center">
  <a href="#configuration">Configuration</a> •
  <a href="#features">Features</a> •
  <a href="#contributing">Contributing</a> •
  <a href="#author">Author</a> •
  <a href="#support">Support</a> •
  <a href="#donate">Donate</a> •
  <a href="#license">License</a>
</p>

---

## About

<table>
<tr>
<td>

**ansible-role-users** is a **high-quality** _Ansible Role_ that deploys **User Accounts** to your ansible clients.

</td>
</tr>
</table>

## Configuration

### Install

```shell
ansible-galaxy install totaldebug.users
```

### Role Variables

#### Main Config

| **Input** | **Default** | **Description** |
|:---------:|:-----------:|:---------------:|
| `users_create_per_user_group` | `true` | when creating users, also create a group with the same username and make that the user's primary group. |
| `users_group` | `users` | if users_create_per_user_group is not set, then this is the primary group for all created users. |
| `users_default_shell ` | `/bin/bash` | the default shell if none is specified for the user. |
| `users_create_homedirs` | `true` | create home directories for new users. Set this to false if you manage home directories separately. |
| `authorized_keys_file ` | `.ssh/authorized_keys` | Set this if the ssh server is configured to use a non standard authorized keys file. |
| `users_ssh_key_exclusive` | `false` | Whether to remove all other non-specified keys from the authorized_keys file. |


#### User Creation

Add a users variable containing the list of users to add. A good place to put this is in `group_vars/all` or `group_vars/groupname` if you only want the users to be on certain machines.

| **Input** | **Default** | **Description** |
|:---------:|:-----------:|:---------------:|
| `username` | | The user's username. |
| `name` | | The full name of the user. |
| `home` | `/home/username` | The home directory of the user to create. |
| `uid ` | | The numeric user id for the user (optional). This is required for uid consistency across systems. |
| `gid` | | The numeric group id for the group (optional). |
| `password` | | If a hash is provided then that will be used, but otherwise the account will be locked. |
| `update_password` | `always` | This can be either 'always' or 'on_create'
'always' will update passwords if they differ.
'on_create' will only set the password for newly created users. |
| `password_lock` | `false` | allows locking users password. |
| `expires` |  | Optional expiry time for the user in epoch, it will be ignored on platforms that do not support this. You can remove the expiry time by specifying a negative value. Currently supported on GNU/Linux and FreeBSD. |
| `group` | | Optional primary group override. |
| `groups` | `[]`| A list of supplementary groups for the user. |
| `append` | `false` | If true, will only add groups, not set them to just the list in groups (optional). |
| `profile` | | A string block for setting custom shell profiles. |
| `ssh_key` | | This should be a list of SSH keys for the user (optional). Each SSH key should be included directly and should have no newlines.
| `generate_ssh_key` | `false` | Whether to generate a SSH key for the user (optional). |
| `shell` | `/bin/bash` | The user's shell. This defaults to /bin/bash. The default is configurable using the users_default_shell variable if you want to give all users the same shell, but it is different than /bin/bash. |
| `system` | `false` | Allows creation of system users. |
| `ssh_key_exclusive` | `users_ssh_key_exclusive` | Whether to remove all other non-specified keys from the authorized_keys file. |

#### Group Creation

| **Input** | **Default** | **Description** |
|:---------:|:-----------:|:---------------:|
| `name` | | The group's name. |
| `gid` | | The numeric group id for the group (optional). This is required for gid consistency across systems. |
| `system` | `false` | Allows creation of system group. |

#### User Deletion

| **Input** | **Default** | **Description** |
|:---------:|:-----------:|:---------------:|
| `username` | | The user's username. |

### Example Configuration

```yaml
---
users:
  - username: terry
    name: Terry Chocolate
    groups: ['sudo', 'systemd-journal']
    uid: 1001
    home: /local/home/terry
    profile: |
      alias ll='ls -lah'
    ssh_key:
      - "ssh-rsa AAAAA.... foo@machine"
      - "ssh-rsa AAAAB.... foo2@machine"
groups_to_create:
  - name: developers
    gid: 2002
users_deleted:
  - username: Orange
```

## Features

|                            |         🔰         |
| -------------------------- | :----------------: |
| Create users          |         ✔️         |
| Delete Users         |         ✔️         |
| Create Groups    |         ✔️         |


## Contributing

Got **something interesting** you'd like to **share**? Learn about [contributing](https://github.com/totaldebug/.github/blob/main/.github/CONTRIBUTING.md).

### Versioning

This project follows semantic versioning.

In the context of semantic versioning, consider the role contract to be defined by the role variables.

- Breaking Changes or changes that require user intervention will increase the major version. This includes changing the default value of a role variable.
- Changes that do not require user intervention, but add new features, will increase the minor version.
- Bug fixes will increase the patch version.

## Author

| [![TotalDebug](https://totaldebug.uk/assets/images/logo.png)](https://linkedin.com/in/marksie1988) |
|:--:|
| **marksie1988 (Steven Marks)** |

## Support

Reach out to me at one of the following places:

- via [Discord](https://discord.gg/6fmekudc8Q)
- Raise an issue in GitHub

## Donate

Please consider supporting this project by sponsoring, or just donating a little via [our sponsor page](https://github.com/sponsors/marksie1988)

## License

[![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-orange.svg?style=flat-square)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

- Copyright © [Total Debug](https://totaldebug.uk "Total Debug").
