# Application Lifecycle Management with Jenkins CI/CD

## Objective

Set up environment for application lifecycle management using Ansible, Jenkins, Maven, and Spring.

## Quickstart

Create Python virtualenv:

```
mkvirtualenv jalm
```

Install Ansible:

```
pip install Ansible
```

Install Ansible Galaxy roles:

```
cd ansible
ansible-galaxy install -r requirements.yml
```

Create and provision Vagrant box:

```
vagrant plugin install vagrant-hostmanager
vagrant up
```

Connect to Jenkins:

- http://192.168.1.10:8080/
- l/p: admin/admin		(can be set in [ansible/vars/main.yml](ansible/vars/main.yml))
