# How to setup Diaspora Development Environment with Vagrant

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
