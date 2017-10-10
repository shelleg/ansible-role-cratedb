CrateDB Role
============

A naive (AMT) role to install a single CrateDB instance for purposes of serving as a prometheus long-term storage solution.
In addition should support [prometheus / cratedb_adapter](https://github.com/crate/crate_adapter) (still WIP)

Requirements
------------

It's all included ;)
You probably want to use together with [shelleg.prometheus](https://github.com/shelleg/ansible-role-prometheus)
Fully tested on Centos7 see ./tests directory
Still having minor issues with Xenial so still WIP

Role Variables
--------------

Flags / features:
* `cratedb_prometheus_init: false` - if set to true will connect to crate and create a `metrics table`
* 'cratedb_adapter_testing: false' - if set to true will install from testing repository ( needed 2.2.x for prometheus adapter to work)

* `cratedb_user: crate`
* `cratedb_group: crate`
* `cratedb_listen_address: 0.0.0.0`
* `cratedb_listen_port: 4200`
* `cratedb_config_dir: /etc/crate/`

Dependencies
------------

None !

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - role: shelleg.cratedb

Once Ansible run is complete:
-----------------------------

Get Crate's admin UI vi http://{{ ansible_hostname }}:4200/admin in your browser.

License
-------

[Apache 2](https://choosealicense.com/licenses/apache-2.0/)


Author Information
------------------

[Haggai Philip Zagury](http://www.tikalk.com/devops/haggai)
