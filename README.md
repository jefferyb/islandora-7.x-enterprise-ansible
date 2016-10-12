# Islandora 7.x.Enterprise: Ansible

This ansible playbook will install and configure [an Enterprise version of Islandora 7.x.](https://wiki.duraspace.org/display/ISLANDORA/Enterprise)

This ansible playbook has been tested using Ubuntu 14.04 and 16.04 but recommanded to use Ubuntu 14.04

# Setup

Clone this repository locally, edit `hosts` in install-islandora-7.x-enterprise.yaml to where you want to install.

```bash
git clone https://github.com/jefferyb/islandora-7.x-enterprise-ansible.git
cd islandora-7.x-enterprise-ansible
ansible-playbook install-islandora-7.x-enterprise.yaml
```

If you want to switch some settings, edit `islandora-7.x-enterprise-ansible/group_vars/all`

# Contributing

I'm still new to the project, learning the ins & outs, so if you use it and find some bugs or way to improve the setup,
please don't hesitate to contact me/contribute...
