[![Build Status](https://travis-ci.org/antoiner77/caddy-ansible.svg?branch=master)](https://travis-ci.org/antoiner77/caddy-ansible)
[![Galaxy Role](https://img.shields.io/badge/role-antoiner77.Caddy-blue.svg)](https://galaxy.ansible.com/detail#/role/6801)

Caddy Ansible Role
=========

This role installs and configures the caddy web server. The user can specify any http configuration parameters they wish to apply their site. Any number of sites can be added with configurations of your choice.

Dependencies
------------
None

Role Variables
--------------

**The [Caddyfile](https://caddyserver.com/docs/caddyfile)** (notice the pipe)<br>
default:
```
caddy_config: |
  localhost:2020
  gzip
  root /var/www
  git github.com/antoiner77/caddy-ansible /
```
**Email is used for the lets encrypt integration:**<br>
example:
```
caddy_email: foo@foo.bar
```
**Auto update Caddy?**<br>
default:
```
caddy_update: yes
```
**Features that can be added to core:** cors,git,hugo,ipfilter,jsonp,search<br>
default:
```
caddy_features: git
```

Example Playbook
----------------
```
---
- hosts: all
  roles:
    - role: caddy-ansible
      caddy_email: foo@foo.bar
      caddy_config: |
        localhost:2020
        gzip
        root /var/www
        git github.com/antoiner77/caddy-ansible /
```

Debugging
---------
If the service fails to start you can figure out why by looking at the output of Caddy.<br>
**Upstart (ubuntu, debian wheezy, centos/rhel 6)**<br>
`tail /var/log/upstart/caddy.log`<br>
**Systemd (debian jessie, centos/rhel 7)**<br>
`systemctl status caddy -l`

If something doesn't seem right, open an issue!

Contributing
------------
Pull requests are welcome. Please test your changes beforehand with vagrant:
```
vagrant up
vagrant provision (since it already provisioned there should be no changes here)
vagrant destroy
```