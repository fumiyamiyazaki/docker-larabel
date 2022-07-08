# docker-larabel

# app コンテナに入ります。
$ docker compose exec app bash

# 書き込み権限がないとキャッシュやログにエラーを書き込めないので、権限を付与しておきます。
[app] $ chmod -R 777 storage bootstrap/cache

# vendor ディレクトリへライブラリ群をインストールします。
[app] $ composer install

# .envの有無の確認
[app] $ ls -l

# .env.exampleはあるので .env.example を元にコピーして作成します。
[app] $ cp .env.example .env

# localhost:8080を開いてエラー確認
# エラーメッセージはログと同じく .env に APP_KEY= の値がないと出る。
# アプリケーションキーを生成。
[app] $ php artisan key:generate

# localhost:8080を開く
# public/storage から storage/app/public へのシンボリックリンクを張ります。
# システムで生成したファイル等をブラウザからアクセスできるよう公開するためにシンボリックリンクを張ってます。
[app] $ php artisan storage:link

# 最後にマイグレーションを実行して適用されればOK。
[app] $ php artisan migrate
