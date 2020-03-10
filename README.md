# rails-dockerfile

## 作成環境

* rails:6.0
* mysql:8.0
* ruby:2.6

## ファイル構成

```
.
├── docker-compose.yml
├── Dockerfile 
├── Gemfile
└── Gemfile.lock

```

## 環境構築のやり方

```
1.docker-compose run web rails new . --force --no-deps --database=mysql --skip-test --webpacker

2.docker-compose build

3.docker-compose up

4.config/detabase.yml

default: &default
  adapter: mysql2
  encoding: utf8mb4
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: <%= ENV.fetch("MYSQL_USERNAME", "root") %>
  password: <%= ENV.fetch("MYSQL_PASSWORD", "password") %>
  host: <%= ENV.fetch("MYSQL_HOST", "db") %>

development:
  <<: *default
  database: myapp_development

test:
  <<: *default
  database: myapp_test

production:
  <<: *default
  database: myapp_production
  username: myapp
  password: <%= ENV['MYAPP_DATABASE_PASSWORD'] %>


5.docker-compose run web rake db:create

========================================
  Your Yarn packages are out of date!
  Please run `yarn install --check-files` to update.
========================================

エラーがでたら……

config/webpacker.ymlのcheck_yarn_integrityをfalseに修正

# Verifies that correct packages and versions are installed by inspecting package.json, yarn.lock, and node_modules
check_yarn_integrity: false


6.docker-compose up

```