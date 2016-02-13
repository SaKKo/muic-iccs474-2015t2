# ICCS474
## Internet Programming

## Rails Additional Features

- Elastic Search
    - `brew install elasticsearch`
    - `gem 'searchkick'`

- Moving to Postgres
    - download `postgresapp` for mac
    - Check command line documentation in postgresapp
        - you should be able to run `psql` if you opened a new terminal tab.
        - `\q` to exit from `psql`
    - run (read the config below first)
        - `$ createdb #{YOUR_DB_NAME}_#{environment}`
        - `$ createuser #{YOUR_USER_NAME}`
        - `$ psql`
        - `> alter user #{YOUR_USER_NAME} with encrypted password '#{YOUR_PASSWORD}';`
        - `> alter user #{YOUR_USER_NAME} superuser;`
        - `\q`
    - add `gem pg` then `bundle install`
    - try `rake db:migrate`
    - your `config/database.yml`

```
    default: &default
      adapter: postgresql
      encoding: unicode
      pool: 25
      username: YOUR_USER_NAME
      password: YOUR_PASSWORD
      port: 5432
      reconnect: true
      variables:
        tcp_keepalives_idle: 60
        tcp_keepalives_interval: 60
        tcp_keepalives_count: 100

    development:
      <<: *default
      host: localhost
      database: YOUR_DB_NAME_development

    # Warning: The database defined as "test" will be erased and
    # re-generated from your development database when you run "rake".
    # Do not set this db to the same as development or production.
    test:
      <<: *default
      host: localhost
      database: YOUR_DB_NAME_test

    production:
      <<: *default
      host: localhost
      database: YOUR_DB_NAME_production
```
