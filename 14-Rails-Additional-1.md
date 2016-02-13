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
