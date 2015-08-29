# omnibus-ansible
Install latest Ansible via pip + dependencies via a shell script

This file is used to install ansible in test kitchen when you set in the kitchen.yaml file
require_ansible_omnibus: true 

By default test kitchen will always download and use the latest version of this install file. 

WARNING: AS SOON AS YOU MERGE CODE HERE IT IS INSTANTLY AVAILABLE TO EVERYONE DOING OMNIBUS KITCHEN ANSIBLE INSTALLS:

To get a previous version or lock the install script to a particular version update your kitchen.yaml file to: 
ansible_omnibus_url: https://raw.githubusercontent.com/neillturner/omnibus-ansible/ab2fa5771b6ef357786d7ff57d83fc8c97c22fed/ansible_install.sh

where ab2fa5771b6ef357786d7ff57d83fc8c97c22fed is the commit sha of the code. 

Feel free to fork this repo and create custom install scripts. 
