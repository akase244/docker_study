# docker_study

## usage for ruby
1. Create new Rails project
    ```
    $ docker-compose run web rails new . --force --database=mysql
    Creating network "ruby_default" with the default driver
    Creating ruby_db_1 ... done                                                                                             
    ・
    ・
    ・
    Bundle complete! 18 Gemfile dependencies, 78 gems now installed.
    Use `bundle info [gemname]` to see where a bundled gem is installed.
             run  bundle exec spring binstub --all
    * bin/rake: spring inserted
    * bin/rails: spring inserted
    ```

1. Install gem files
    ```
    $ docker-compose build
    db uses an image, skipping
    Building web
    Step 1/8 : FROM ruby:2.5.1
     ---> 1624ebb80e3e
    ・
    ・
    ・
    Successfully built e3dfeb629b59
    Successfully tagged ruby_web:latest
    ```

1. Modify `config/database.yml`
    ```
    18c18
    <   host: db
    ---
    >   host: localhost
    ```

1. Start Docker containers
    ```
    $ docker-compose up -d
    ruby_db_1 is up-to-date
    Creating ruby_web_1 ... done
    ```

1. Check running Docker containers
    ```
    $ docker-compose ps
       Name                 Command               State            Ports
    -----------------------------------------------------------------------------
    ruby_db_1    docker-entrypoint.sh mysqld      Up      0.0.0.0:13306->3306/tcp
    ruby_web_1   bundle exec rails s -p 300 ...   Up      0.0.0.0:3000->3000/tcp
    ```

1. Create databases.
    ```
    $ docker-compose run web bundle exec rake db:create
    Starting ruby_db_1 ... done
    Created database 'app_development'
    Created database 'app_test'
    ```

1. Open URL.
    ```
    http://localhost:3000/
    ```
