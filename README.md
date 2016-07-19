# omnibus-ansible
Install latest Ansible via pip + dependencies via a shell script

This file is used to install ansible in test kitchen when you set in the kitchen.yaml file

require_ansible_omnibus: true 

By default test kitchen will always download and use the latest version of this install file. 

WARNING: AS SOON AS YOU MERGE CODE HERE IT IS INSTANTLY AVAILABLE TO EVERYONE DOING OMNIBUS KITCHEN ANSIBLE INSTALLS:

To get a previous version or lock the install script to a particular version update your kitchen.yaml file to: 
ansible_omnibus_url: https://raw.githubusercontent.com/neillturner/omnibus-ansible/ab2fa5771b6ef357786d7ff57d83fc8c97c22fed/ansible_install.sh

where ab2fa5771b6ef357786d7ff57d83fc8c97c22fed is the commit sha of the code. 

Supported platforms:

 - `centos-5.10` - Fails due to `pip` not working on python 2.4.. [this article provides a workaround](https://coderwall.com/p/lbr5pg/fixing-ansible-python-2-6-dependency-on-for-rhel-centos-5), but it seemed risky and wouldn't reflect most user's reality of running Ansible on CentOS 5.
 - `centos-6.4` - Works!  (Note: Has `procps` instead of `procps-ng`)
 - `centos-6.5` - Works!  (Note: Has `procps` instead of `procps-ng`)
 - `centos-7.0` - Works!  (Note: Has `procps-ng` instead of `procps`)
 - `ubuntu-10.04` - Fails due to `pycrypto` conflict
 - `ubuntu-12.04` - Works!
 - `ubuntu-14.04` - Works!
 - `ubuntu-14.10` - Works!
 - `ubuntu-15.04` - Works!
 - `ubuntu-16.04` - Works!
 - `debian-6.0.8` - Works!
 - `debian-6.0.10` - Works!
 - `debian-7.8` - Works!
 - `debian-8.1` - Works!


It does some basic OS detection and tries to install all the things that Ansible needs, including some optional packages which are technically dependencies of some core Ansible modules (Ansible playbooks that use these modules would simply fail without them). 

It also installs `ca-certificates` and has built-in yum failure retry ability (With RHEL / CentOS, this is important because `yum` tends to fail a lot due to stale cache and old SSL CA cert chain issues).  It also tries to install via packaged `python-pip`, and if that fails, it tries `easy_install pip`.

This ends up being a lot of things to install (mainly due to optional Ansible module dependencies), but the hope is that it covers all the bases so that some Ansible modules don't just fail unexpectedly. 

The tradeoff is the amount of download / install time this takes versus a more minimal install.  This useful to avoid having to bootstrap Ansible's dependencies using a pre-role or `pre_tasks:` in the test playbook when just testing one playbook or role without redoing the same work that already done in this script. 

This script was built with reliability, resiliency, and installing all "full-stack" dependencies (hence: [Omnibus](https://github.com/chef/omnibus)) in mind, not speed.


Feel free to fork this repo and create custom install scripts. 
