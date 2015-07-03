# How to setup Diaspora Development Environment with Vagrant

This is an updated Guide for using [diaspora* -replica](https://github.com/joebew42/diaspora-replica)

[Original Gide](https://wiki.diasporafoundation.org/Installation/Vagrant_puppet_capistrano)

- [How to setup Diaspora Development Environment with Vagrant](#how-to-setup-diaspora-development-environment-with-vagrant)
	- [Initialize project](#initialize-project)
	- [Cloning your git repository in src/ directory](#cloning-your-git-repository-in-src-directory)
	- [Run development virtual machine](#run-development-virtual-machine)
	- [Enabling vagrant user to use rvm (first time set up)](#enabling-vagrant-user-to-use-rvm-first-time-set-up)
	- [Prepare the Rails application](#prepare-the-rails-application)
	- [Configure Rubies and Gemsets](#configure-rubies-and-gemsets)
	- [Install gems and create databases](#install-gems-and-create-databases)
	- [Configure test environment](#configure-test-environment)
	- [Run all tests](#run-all-tests)
	- [How to upgrade diaspora*-replica](#how-to-upgrade-diaspora-replica)
	- [How to update your forked diaspora repository](#how-to-update-your-forked-diaspora-repository)

- [Configure Git to sync your fork with the original diaspora repository](#configure-git-to-sync-your-fork-with-the-original-diaspora-repository)

## Configure FQDNs in your system

Vagrantfile, Puppet and Capistrano are already configured to handle three kind of environment: development, staging and production. If you want to try them you have to update /etc/hosts file, adding to it the three FQDN for the local diaspora* installation.

Put these entries in your /etc/hosts :
```
192.168.11.2    development.diaspora.local
192.168.11.3    staging.diaspora.local
192.168.11.4    production.diaspora.local
```
## Initialize project
```
git clone https://github.com/joebew42/diaspora-replica.git
cd diaspora-replica/
git submodule update --init
```

## Cloning your git repository in src/ directory
```
cd diaspora-replica/
git clone your_own_diapora_git_repo src
```

## Run development virtual machine
```
vagrant up development
```

## Enabling vagrant user to use rvm (first time set up)
```
vagrant ssh development
vagrant@development:~$ sudo usermod -aG rvm vagrant && newgrp rvm
vagrant@development:~$ /bin/bash --login
```

## Prepare the Rails application

```
vagrant@development:~$ cd diaspora_src
```
## Configure Rubies and Gemsets
```
vagrant@development:~$ rvm use 2.2.2
vagrant@development:~$ rvm gemset create diaspora_dev
vagrant@development:~$ rvm gemset use diaspora_dev
```
## Install gems and create databases

**important**: use bundler >= 1.10 and do

``
bundle install --with mysql
``
for MySQL support

and

 ``
bundle install --with postgresql
 ``
for PostgreSQL support

```
vagrant@development:~$ rake generate:secret_token
vagrant@development:~$ rake db:create
vagrant@development:~$ rake db:migrate
```
## Configure test environment
```
vagrant@development:~$ rake db:test:prepare
vagrant@development:~$ bin/rake assets:generate_error_pages
```

## Run all tests
``
vagrant@development:~$ rspec
``

## How to upgrade diaspora*-replica

```
cd diaspora-replica/
git pull --rebase origin master
git submodule update

vagrant up production
vagrant provision production --provision-with puppet

cd capistrano/
cap production deploy
cap production foreman:restart
```

## How to update your forked diaspora repository
### Configure Git to sync your fork with the original diaspora repository
check your current remote setup
``
git remote -v
``
add original repository
``
git remote add upstream https://github.com/diaspora/diaspora.git
``

sync your fork to current develop branch
```
git fetch upstream
git checkout develop
git merge upstream/develop
```
