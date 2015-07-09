# * Workflow

## start development enviroment

start redis

``redis-server /usr/local/etc/redis.conf``

start mysql

``mysql.server start``

start diaspora

``script/server``


### reset database to a clean state
``   bin/rake db:drop db:create db:schema:load ``

## Testing Workflow

### RSpec
```
RAILS_ENV="test" bin/rake db:create db:schema:load
bin/rake spec
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

