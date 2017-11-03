
### BU Obseques

 *Ansible Deployment Tool*



## What is Ansible

Principle : It just runs over SSH to the destination server

- Python package, come with modules
- Uses Python-paramiko
- Needs Python >=2.4
- No agent installed on remote server

To see Ansible installation, see bottom slide.


#### How to install Ansible

You will need ```python-pip``` package :

```
apt-get update; apt-get install -y python-pip
pip install ansible
```



#### Actual use case

One playbook and one hosts file by website

Drawbacks :
 - Most of the hosts are duplicated
 - Reduce clarity/readability
 - Build tasks are 'nearly' the same.


#### Actual project tree structure
```
espacepro-precom-obseques/
├── group_vars
│   ├── all
│   │   └── vars_all.yml
│   ├── env_dev
│   │   └── vars.yml
│   ├── env_prod
│   │   └── vars.yml
│   └── env_qual
│       └── vars.yml
├── hosts
│   ├── dev
│   ├── prod
│   └── qual
├── playbook.yml
└── tasks
    ├── clone.yml
    ├── container.yml
    ├── deploy.yml
    └── prepare_archive.yml
```



#### Improvement perspectives

 - Most of container build tasks could be centralized
 - Create centralized roles to be used by each playbook


#### Proposal of new project tree structure

```
├── espacepro-precom-obseques
│   ├── group_vars
│   │   ├── all
│   │   │   └── vars_all.yml
│   │   ├── env_dev
│   │   │   └── vars.yml
│   │   ├── env_prod
│   │   │   └── vars.yml
│   │   └── env_qual
│   │       └── vars.yml
│   ├── playbook.yml
│   └── tasks
│       ├── clone.yml
│       ├── container.yml
│       ├── deploy.yml
│       └── prepare_archive.yml
├── hosts
│   ├── dev
│   ├── prod
│   └── qual
├── pagesObseques
│   ├── group_vars
│   │   ├── all
│   │   │   └── vars_all.yml
│   │   ├── env_dev
│   │   │   └── vars.yml
│   │   ├── env_prod
│   │   │   └── vars.yml
│   │   └── env_qual
│   │       └── vars.yml
│   ├── playbook.yml
│   ├── tasks
│   │   ├── clone.yml
│   │   ├── container.yml
│   │   ├── deploy.yml
│   │   └── prepare_archive.yml
│   └── templates
│       └── pagesObseques.j2
```


#### What is Ansible role

An ansible role is often composed of following folders :
 - tasks/ : main yaml tasks
 - defaults/ : default variables for role, can be overrided by playbook which use role (or by user)
 - templates/ : Jinja2 files, useful to copy files containing variables
