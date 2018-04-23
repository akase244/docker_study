# docker_study

```
$ docker-compose run web rails new . --force --database=mysql

$ docker-compose build

$ vim config/database.yml

before
  default: &default
    adapter: mysql2
    encoding: utf8
    pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
    username: root
    password:
    host: localhost

after
  default: &default
    adapter: mysql2
    encoding: utf8
    pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
    username: root
    password:
    host: db

$ docker-compose up -d

$ docker-compose ps

$ docker-compose run web bundle exec rake db:create

access to http://localhost:3000/
```
