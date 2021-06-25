# FROM命令はイメージビルドのためのベースイメージを設定します。
# FROM イメージ名:タグ名 で指定します。
FROM php:8.0-fpm-buster
# SHELL命令は何も指定しない場合は SHELL ["/bin/sh", "-c"] がデフォルト値となります(Linuxの場合)
SHELL ["/bin/bash", "-oeux", "pipefail", "-c"]
# コンテナ内のサーバー環境変数を設定します。
ENV COMPOSER_ALLOW_SUPERUSER=1 \
  COMPOSER_HOME=/composer
# COPY 命令は <src> からファイルやディレクトリを新たにコピーして、コンテナー内のファイルシステムのパス <dest> に追加します。
COPY --from=composer:2.0 /usr/bin/composer /usr/bin/composer
# RUN 命令は、現在のイメージの最上位の最新レイヤーにおいて、あらゆるコマンドを実行します。 そして処理結果を確定します。 結果が確定したイメージは、Dockerfile の次のステップにおいて利用されていきます。
RUN apt-get update && \
  apt-get -y install git unzip libzip-dev libicu-dev libonig-dev && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* && \
  docker-php-ext-install intl pdo_mysql zip bcmath
COPY ./php.ini /usr/local/etc/php/php.ini
# WORKDIR 命令はワークディレクトリを設定します。
WORKDIR /work