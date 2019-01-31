Example playbook for Sentry
===========================

This is a playbook for a small talk I gave at Unleashed NV. It is a real life example for setting up Sentry on Vagrant boxes.

The Vagrantfile has 2 machines for testing purposes: Ubuntu 18.04/bionic and CentOS 7.

Requirements
------------

- [Ansible](https://docs.ansible.com/)
- [Vagrant](https://www.vagrantup.com/)
- [VirtualBox](https://www.virtualbox.org/)
- this git repo + submodules

I've been working from a macOS machine, here are the installation instructions with [Homebrew](https://brew.sh/):

    brew install ansible
    brew cask install virtualbox
    brew cask install vagrant

    git clone git@github.com:Duologic/ansible-playbook-sentry.git
    git submode update --init

Let's go
--------

You should now have an environment that would allow you to spin up a sentry server:

    vagrant up sentry1

Surf to https://localhost:9000/

License
-------

MIT

Author Information
------------------

Jeroen Op 't Eynde, jeroen@simplistic.be
