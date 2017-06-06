# Vagrant: Template Debian VM

Vagrant config to clone and use in testing environement.  
Box designed to test ansible playbooks, so it uses ansible provisioning.  

## Options

Box is cofigurable with environement variables:

* `BOX` - box image to use. Any box image can be used. **Default:** `debian/jessie64`
* `OS`  - OS to start. Alternative to `BOX` option. Only *`Ubuntu`* value is supported.
* `BOX_NAME` - VM name and hostname. **Default:** `ansible-snp`
* `BOX_USER` - User to login with. **Default:** `ubuntu` for Ubuntu, `vagrant` - for any other boxes.
* `BOX_ANSIBLE` - Path to ansible playbooks and roles. **Default:** `./ansible/`
* `BOX_PLAYBOOK` - Playbook filename to provision VM with. **Default:** `vagrant.yaml`

## Example
Start Debian box with default settings:
> `$ vagrant up`  

Start Ubuntu box with default settings:
> `$ OS=Ubuntu vagrant up`

Start Ubuntu box with hostname `test` and `test.yaml` playbook to provision it:
> `$ OS=Ubuntu BOX_NAME=test BOX_PLAYBOOK=test.yaml vagrant up`