FROM php:5.6.30-fpm

#ブラウザ上にphpのエラー内容を出力させない場合は下記を有効化する
#COPY app/conf/disable_display_error.ini $PHP_INI_DIR/conf.d/

#php.iniの設置
COPY app/conf/php.ini $PHP_INI_DIR/conf.d/php.ini

#php-fpm用confファイルコピー
COPY app/conf/zz-docker.conf /usr/local/etc/php-fpm.d/

#コンテナ実行ユーザーとグループをrootから変更
RUN groupmod -g 1000 www-data
RUN usermod -u 1000 www-data

#イメージのベースOSが古すぎて404になるため、updateは実施しない
#また、apt-get update を実施できないため、git や redis のインストールもできない
#apt-get update -y && apt-get install -y git && git clone https://github.com/phpredis/phpredis.git /usr/src/php/ext/redis && docker-php-ext-install redis

#ドキュメントルート作成
RUN docker-php-ext-install pdo_mysql && \
    mkdir -p /var/www/vhosts/www.example.com/public_html

COPY ./app/src /var/www/vhosts/www.example.com/public_html

#ドキュメントルートの権限変更
RUN chown -R www-data:www-data /var/www/vhosts/www.example.com/public_html

# ユーザー切り替え
USER www-data

#作業ディレクトリ設定
WORKDIR /var/www/vhosts/www.example.com/public_html

#ポート開放
EXPOSE 9000
