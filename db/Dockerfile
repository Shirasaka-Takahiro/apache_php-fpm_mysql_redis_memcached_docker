FROM mysql:5.6.36

#もしイメージ作成時に初期DBやユーザーを作成したい場合は下記を有効化する
#COPY db/sql /docker-entrypoint-initdb.d

COPY db/conf/my.cnf /etc/my.cnf

EXPOSE 3306
