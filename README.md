# ElasticsearchAutocomplete

[![Build Status](https://travis-ci.org/leschenko/elasticsearch_autocomplete.png?branch=master)](https://travis-ci.org/leschenko/elasticsearch_autocomplete)
[![Dependency Status](https://gemnasium.com/leschenko/elasticsearch_autocomplete.png)](https://gemnasium.com/leschenko/elasticsearch_autocomplete)

Simple autocomplete for rails models using awesome [Elasticsearch](http://www.elasticsearch.org/).

## Example app

Look at ElasticsearchAutocomplete [example app](https://github.com/leschenko/example_elasticsearch_autocomplete)

## Installation

Add this line to your application's Gemfile:

    gem 'elasticsearch_autocomplete'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install elasticsearch_autocomplete

## Basic Usage

Specify attributes for autocompletion. By default, this is `name` attribute:

```ruby
class User < ActiveRecord::Base
  ac_field :full_name
end
```

Don't forget to rebuild elasticsearch index:

```bash
    $ rake environment tire:import CLASS='User' FORCE=true
```

To find suggestions call `ac_search` method on your model. It return `Tire::Results::Collection` instance:

```ruby
User.ac_search('Alex').map(&:full_name)
=> ['Alex First', 'Alexandr Second']
```

##

You can specify fields for suggestions search:

```ruby
class User < ActiveRecord::Base
  ac_field :full_name, search_fields: [:full_name, :email]
end
```

For search on localized fields such as `name_en`, `name_ru`:

```ruby
class Product < ActiveRecord::Base
  ac_field :name, localized: true
end
```

If you want to define settings and mapping for elasticsearch index yourselves:

```ruby
class Product < ActiveRecord::Base
  ac_field :name, skip_settings: true
end
```

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
