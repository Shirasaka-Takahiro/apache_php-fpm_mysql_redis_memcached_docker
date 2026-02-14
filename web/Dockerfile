#ローカルでコンバートしたイメージを指定
FROM httpd:2.4.16

#デフォルトのconfファイルでは下記パスのみ設定されているので、下記以外のパスでドキュメントルートを作成する場合は <Directory> で別途ドキュメントルートパスを指定する必要あり
#<Directory "/usr/local/apache2/htdocs">

#デフォルトで下記includeはコメントアウトされているので、デフォルトのconfを書き換える必要がある
# Virtual hosts
#Include conf/extra/httpd-vhosts.conf

#デフォルトのconfファイルを上書き
COPY web/conf/httpd.conf /usr/local/apache2/conf/httpd.conf

#追加のvhost用confファイルをコピー
COPY web/conf/www.example.com.conf /usr/local/apache2/conf/extra

#コンテナ実行ユーザーとグループをrootから変更
RUN groupmod -g 1000 www-data
RUN usermod -u 1000 www-data

#ドキュメントルート作成
RUN apt-get update -y && apt-get install less && mkdir -p /var/www/vhosts/www.example.com/public_html

#appコンテナ配下のソースコードをコピー
COPY ./app/src /var/www/vhosts/www.example.com/public_html

#ドキュメントルートとPIDの権限変更
RUN chown -R www-data:www-data /var/www/vhosts/www.example.com/public_html && \
    chown -R www-data:www-data /usr/local/apache2/logs

# ユーザー切り替え
USER www-data

#作業ディレクトリ設定
WORKDIR /var/www/vhosts/www.example.com/public_html

#ポート開放
EXPOSE 80
