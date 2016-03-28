source 'https://rubygems.org'
ruby '2.3.0'

gem 'inherited_resources', '~> 1.6.0'
gem 'bundler', '~> 1.9.6'
gem 'rails', '~> 4.2.6'
gem 'rails_12factor', '~> 0.0.3'
gem 'rake', '~> 10.4.2'
gem 'unicorn', '~> 4.9.0'
gem 'pg', '~> 0.18.2'
gem 'elasticsearch-rails'
gem 'rails-settings-cached', '0.4.1'
gem 'sidekiq', '~> 2.12.0'
gem 'sidekiq-failures', '~> 0.2.2'
gem 'ruby-progressbar', '~> 1.1.0'
gem 'redcarpet', '~> 3.1.2'
gem 'faker', '~> 1.4.2'
gem 'axlsx_rails', '~> 0.2.0'
gem 'dalli', '~> 2.6.4'
gem 'memcachier', '~> 0.0.2'
gem 'rakismet', '~> 1.5.0'
gem 'htmlentities', '~> 4.3.2'
gem 'activerecord-session_store', '~> 0.1.1'
gem 'daemons', '~> 1.0.10'
gem 'sanitize', '~> 2.0.3'
gem 'will_paginate', '~> 3.0'
gem 'thin', '~> 1.5.0'
gem 'amatch', '~> 0.2.11'
gem 'strip_attributes', '~>1.5.1'
gem 'active_model_serializers', '~> 0.8.1'
gem 'rapns', '~> 3.4.1'
gem 'paperclip', '~> 4.3.1'
gem 'aws-sdk', '~> 1.64.0'
gem 'slim', '~> 1.3.0'
gem 'sinatra', '~> 1.3.0', :require => nil
gem 'asset_sync', '~> 1.1.0'

group :developement, :test do
  gem 'm', '~> 1.3.4'
  gem 'factory_girl_rails', '~> 4.5.0'
  gem 'minitest-rails', '~> 2.1.1'
end

group :assets do
  gem 'sass', '~> 3.4.21'
  gem 'sass-rails', '~> 5.0.4'
  gem 'coffee-rails', '~> 4.1.1'
  gem 'uglifier', '~> 3.0.0'
  gem 'jquery-rails', '~> 4.1.1'

  # Rails 4.2 by default uses sprockets 3.1+. There are issues with asset compilation in this
  # version of sprockets related to gzip. Be aware that we should update this gem A.S.A.P.
  # https://github.com/rumblelabs/asset_sync/issues/304
  # https://github.com/rails/sprockets/issues/26
  # gem 'sprockets', '~> 2.12.3'
end