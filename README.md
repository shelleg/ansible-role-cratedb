![picture alt](https://res.cloudinary.com/siftery/image/upload/v1443450475/v1/p/products/crateio.png?imageView/2/w/100/h/100/q/80/format/png "CreateDB") CrateDB Role
============

A naive (ATM) role to install a single CrateDB instance for purposes of serving as a prometheus long-term storage solution.
In addition should support [prometheus / cratedb_adapter](https://github.com/crate/crate_adapter) (still WIP) - This moved to [shelleg.prometheus](https://github.com/shelleg/ansible-role-prometheus)

Requirements
------------

It's all included ;)
You probably want to use together with [shelleg.prometheus](https://github.com/shelleg/ansible-role-prometheus)
Fully tested on Centos7 & Ubuntu-16.04 see ./tests directory

Role Variables
--------------

Flags / features:
* `cratedb_adapter_prometheus_init: false` - if set to true will connect to crate and create a `metrics table`
* 'cratedb_adapter_testing: false' - if set to true will install from testing repository ( needed 2.2.x for prometheus adapter to work)

* `cratedb_user: crate`
* `cratedb_group: crate`
* `cratedb_listen_address: 0.0.0.0`
* `cratedb_listen_port: 4200`
* `cratedb_config_dir: /etc/crate/`

Dependencies
------------
None !

Testing this Role
-----------------

travis-ci should be active using ansible-test-shim with docker see the `.travis.yml` at the root of this directory + the `tests` directory.

In addition for more complex testing you can use the `Vagrantfile` + `servers.yml` under the `test` folder:

The `servers.yml` alongside `Vagrantfile` allows to control

 various aspects of Vagrant see the entire `Vagrantfile` for further details / see a small sample below:


    srv.vm.provision :ansible do |ansible|
         ansible.limit = servers[:name]
      if servers["playbook"] == nil
         ansible.playbook = "./test.yml"
      else
         ansible.playbook = "./#{servers["playbook"]}"
      end
      if servers["inventory"] != nil
         ansible.inventory_path = servers["inventory"]
      end
          ansible.sudo = "true"
          ansible.sudo_user = "root"
          ansible.host_key_checking = "false"
          ansible.verbose = "-v"
          # in case we have requirements for ansible role under development
          ansible.galaxy_roles_path = "./site-roles/"
          # requirements file
          ansible.galaxy_role_file = "./requirements.yml"
          # extra_vars
          ansible.extra_vars = {
            some_var: "some_value",
            dict: {
              kay1: "val1",
              kay2: "val2"
            }
          }
    end


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - role: shelleg.cratedb

Once Ansible run is complete:
-----------------------------

Get Crate's admin UI vi `http://{{ ansible_hostname }}:4200/admin` in your browser.


License
-------

[![GitHub license](https://img.shields.io/github/license/shelleg/ansible-role-cratedb.svg?style=plastic)](https://github.com/shelleg/ansible-role-cratedb/blob/master/LICENSE)


Author Information
------------------

[Haggai Philip Zagury](http://www.tikalk.com/devops/haggai)
