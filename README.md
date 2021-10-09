# docker-laravel-handson

やったこと
１．作業ディレクトリ(docker-laravel-handson)作成
２．appコンテナの作成(Dockerfileから生成)
  ①Docker-compose.yml編集
    PC側backend と　コンテナ側workをマウント
  ②Dockerfileの編集
    ・PHPイメージのインストール(php:8.0-fpm-buster)
    ・Composerコマンドをインストール(copy --from=composer:2.0 /usr/bin/composer /usr/bin/composer)
    ・拡張ライブラリををインストール(git,unzip,libzip-div,libicu-dev,libonig-div)
    ・Laravel稼働に必須のPHP拡張機能をインストール(intl,pdo_mysql,zip,bcmath)
  ③php.iniの編集
３．webコンテナ(nginx)の作成(イメージから作成,nginx:1.20-alpine)
  ①Docker-compose.ymlの編集
    ・PC側backend と　コンテナ側workをマウント
    ・PC側default.conf と コンテナ側default.confをマウント
    ・workディレクトリで作業指示(working_dir: /work)
  ②Laravel稼働要件のnginx設定をdefauld.confに記載
４．Laravelのインストール(appコンテナに入りインストール)
  $ composer create-project --prefer-dist "laravel/laravel=8.*" .
５．db(データベース)コンテナの作成(Dockerfileから生成)
  ①Docker-compose.ymlの編集
    ・PC側 db-store と コンテナ側mysqlディレクトリをマウント
  ②Dockerfileの作成
    ・元イメージ、mysql/mysql-server:8.0
    ・ENV を使用して、環境変数設定
    ・PC側my.cnfをイメージ側にコピー
  ③my.cnfファイルを編集
    ・文字コードの設定
    ・タイムゾーンの設定
    ・ログ設定
６．appコンテナに入りマイグレーション
  ①初回マイグレーション（エラーする、接続拒否エラー）
  ②.env,.env.exampleを編集
  ③再マイグレーション