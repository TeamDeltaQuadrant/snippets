# * Workflow

## usefull other stuff

clear the CAAAAAAACHHHE
```
bin/rake tmp:cache:clear
```

## start development enviroment

start redis

``redis-server /usr/local/etc/redis.conf``

start mysql

``mysql.server start``

start diaspora

``script/server``


### reset database to a clean state
``   bin/rake db:drop db:create db:schema:load ``

## [Testing Workflow](https://wiki.diasporafoundation.org/Testing_Workflow)

### RSpec
```
RAILS_ENV="test" bin/rake db:create db:schema:load
bin/rake spec
```

### Jasmine
```
bin/rake tests:generate_fixtures
bin/rake jasmine
```

## [Git Workflow](https://wiki.diasporafoundation.org/Git_workflow#Rebase_your_development_branch_on_the_latest_upstream)

### Rebase

```
git fetch upstream
# make sure all is committed (or stashed) as necessary on this branch
git rebase -i upstream/develop 359-aspect-names
```

## start development enviroment in Vagrant

start vagrant & ssh to vagrant:

```
$ vagrant up development
$ vagrant ssh development
```

start diaspora:

```
$ script/server
```

open Browser on Mac at:

`` http://192.168.11.2:3000 ``

