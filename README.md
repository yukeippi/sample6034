# sample6034

* 「Unixドメインソケット　/var/run/postgresql/.s.PGSQL.5432で通信を受け付けていますか？」のエラーが出る場合

その環境におけるdatabase.ymlを参照できていない可能性が高い。この例ではcredintialsにデータベースの設定を入れ、参照させることで解消した。

```bash
EDITOR="vim" bin/rails credentials:edit
```

```yaml
db:
  username: postgres
  password: (password)
  host: (database endpoint)
```
  
config/database.ymlを下記のように編集。

```yaml
production:
  <<: *default
  database: sample6034_production
  username: <%= Rails.application.credentials.db[:username] %>
  password: <%= Rails.application.credentials.db[:password] %>
  host:     <%= Rails.application.credentials.db[:host] %>
  port:     5432
```
