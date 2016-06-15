
# rails deploy productuon

## index

1. assets precompile
2. db setting
3. edit config
4. set secret key

---------------------

### assets precompile

`bundle exec rake assets:precompile RAILS_ENV=production`

---------------------

### db setting

#### create db

`bundle exec rake db:create RAILS_ENV=production`

#### migrate db

`bundle exec rake db:migrate RAILS_ENV=production`

---------------------

### set RAILS_SERVE_STATIC_FILES

以下の`RAILS_SERVE_STATIC_FILES`の環境変数にtrueを設定する

config/environments/production.rb

```rb
config.serve_static_files = ENV['RAILS_SERVE_STATIC_FILES'].present?
```

.env
```rb
RAILS_SERVE_STATIC_FILES=true
```

`dotenv-rails`のgemを使うと便利

---------------------

### set secret key

`bundle exec rake secret`で出力された乱数を'config/secrets.yml'にセット

```rb
production:
  secret_key_base: ENV[`RAILS_SECRET_KEY`]
```

```rb
RAILS_SECRET_KEY=09876567899876789....
```
