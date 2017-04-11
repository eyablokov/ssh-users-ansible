# Users management & ssh granting / revoking example with ansible

This is example for managing all of company admin users with ansible for all servers.

It has been tested and used in production with `Ubuntu 16.04`, `Debian 8` & `CentOS 7` virtual servers. Other distros won't likely work at this time.

## What's included?
* Manage all your users with git and ansible
* Disables servers from asking for sudo password
* Disables ssh passworded root access and password login for ssh

## How to setup
`group_vars/all/main.yml` file contains list of company super admins which should gain access to all created servers. Remove example data and put list of your admins over there instead.

Create new folder inside `environments` for certain servers. For example these can be: `production`, `testing` or `client-cluster`.

Then create inventory file for the servers. This is an example:
```
[servers]
xxx.xxx.xxx.xxx
yyy.yyy.yyy.yyy
```
You can use hostnames or ip-addresses here.

Then add people involved with certain environments into:
```
environments/{{your-environment}}/group_vars/all/main.yml
```

## How to deploy
This is how you would deploy all users for environment named `production` initially with user `root`. Please provide your ssh password for ansible.

```console
ansible-playbook main.yml -i environments/production -vv
```

**Notice:** The playbook will work properly if person who granting or revoking accesse can connect to hosts from inventories. Because it's a most used case. If don't, it'll be additional play around with passwords, keys, etc, to get things done by ansible.

## Maintainer
[Evgeniy Yablokov]

## License
MIT
