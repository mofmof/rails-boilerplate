# 初期設定
1. `docker compose build` を実行
2. `docker compose run --rm app gem install rails` を実行
3. `docker compose run --rm app rails new . -d mysql -j esbuild` を実行
4. `config/database.yml` の `default` 内に以下を追記
```
username: <%= ENV['DB_USER'] %>
password: <%= ENV['DB_PASS'] %>
host: <%= ENV['DB_HOST'] %>
```
5. `docker compose up mysql -d` を実行
6. `docker compose run --rm app rails db:create` を実行
7. `docker compose stop mysql` を実行
8. `docker compose up` で起動
9. http://localhost:3000/ にアクセスしてページが表示されれば完了
