
# rails deploy productuon

## precompile

`bundle exec rake assets:precompile RAILS_ENV=production`

## db setting

### create db

`bundle exec rake db:create RAILS_ENV=production`

### migrate db

`bundle exec rake db:migrate RAILS_ENV=production`

## edit config/environments/production.rb

以下の`RAILS_SERVE_STATIC_FILES`の環境変数にtrueを設定する

```rb:config/environments/production.rb
config.serve_static_files = ENV['RAILS_SERVE_STATIC_FILES'].present?
```

```rb:.env
RAILS_SERVE_STATIC_FILES=true
```

`dotenv-rails`のgemを使うと便利
