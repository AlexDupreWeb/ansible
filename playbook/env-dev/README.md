# Install development environment

## Required
On your machine, you must have to use this project:
* `Git` to clone this project
* `Python` to use Ansible
* `Ansible` to install configurations

## Commands

    ansible-playbook -i inventory/localhost playbook/env-dev/install-env-dev.yml --ask-sudo-pass
