#
# web
# apache + php
#

FROM ktahara-base
MAINTAINER ktahara

# ===== Apacheのセットアップ (2.2.15) =====
RUN yum install -y httpd

# RUN mkdir /var/www/vhost
# RUN chmod -R 775 /var/www/

# 設定ファイルを上書き
COPY config/httpd.conf /etc/httpd/conf/httpd.conf
# vhostファイルを配置 :TODO 要確認
# COPY config/vhost.conf /etc/httpd/conf.d/vhost.conf

# 起動 && 自動起動設定ON
RUN /etc/init.d/httpd start
RUN chkconfig httpd on


# ===== PHPのセットアップ (7.0.24) =====
RUN yum -y install --enablerepo=epel libwebp
RUN yum -y install --enablerepo=remi gd-last
RUN yum -y install --enablerepo=remi-php70,remi php php-devel php-mbstring php-mysql php-pdo php-common php-gd

# 設定ファイルを上書き
COPY config/php.ini /etc/php.ini

# コンテナ内のポート番号
EXPOSE 80

# コンテナ内でフォアグラウンドで実行
ENTRYPOINT ["/usr/sbin/httpd"]
CMD ["-D", "FOREGROUND"]