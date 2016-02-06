# ICCS474
## Internet Programming

## Rails Additional Features

- Single Table Inheritance
    - Transportation
        - Types
            - Bus
            - Train
            - Ferry
- Polymorphic
    - POI
        - Informations
            - Hotel
            - Tourist Attraction
            - Spa
            - Restaurant

    - Models Structure
        - Poi   `{name: TEXT}`, `{ has_many: poi_poi_infos }`
        - PoiPoiInfo    `{  poi:references, poi_info_id:integer:index, poi_info_type:string:index }, {belongs_to :poi_info, polymorphic: true}`
        - PoiHotelInfo  `{ room_count: integer }`, `{has_one: poi_poi_info, as: :poi_info}`
        - PoiRestaurantInfo  `{ table_count: integer }`, `{has_one: poi_poi_info, as: :poi_info}`

- Cache

    # Run this command twice in console
    x = Rails.cache.fetch("some_key") do
      puts "not cached"
      [1,2,3,4] # implicit return
      # note: you should use `implicit` return.
      # return [1,2,3,4] # is a bad idea.
    end
    # you should only see 'not cached' once

    # Delete Cache
    Rails.cache.delete("some_key")

    # Delete all Cache
    Rails.cache.clear

    # Caching Model
    poi = Rails.cache.fetch("#{poi.cache_key}") do
      puts "not cached"
      Poi.find(1)
    end

> http://guides.rubyonrails.org/caching_with_rails.html

- Memcache & Redis
    - `brew install redis`
    - `brew install memcache`

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
