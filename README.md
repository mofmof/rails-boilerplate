# 初期設定
1. `docker compose build` を実行
2. `docker compose run --rm app gem install rails` を実行
3. `docker compose run --rm app rails new . -d postgresql -j esbuild` を実行
4. `config/database.yml` の `default` 内に以下を追記
```
username: <%= ENV['DB_USER'] %>
password: <%= ENV['DB_PASS'] %>
host: <%= ENV['DB_HOST'] %>
```
6. `package.json` を修正する
```
,
  "scripts": {
    "build:js": "esbuild app/javascript/*.* --bundle --sourcemap --outdir=app/assets/builds"
  }
```
7. `Procfile.dev` を修正
```
web: bin/rails server -b 0.0.0.0 -p 3000
js: yarn build:js --watch
```
8. `docker compose up postgres -d` を実行
9. `docker compose run --rm app rails db:create` を実行
10. `docker compose stop postgres` を実行
11. `docker compose up` で起動
12. http://localhost:3000/ にアクセスしてページが表示されれば完了
