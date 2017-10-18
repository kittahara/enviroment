#
# web
# Mysql
#

FROM ktahara-base
MAINTAINER ktahara

# ===== Mysqlのセットアップ (7.0.24) =====
RUN yum -y install --enablerepo=epel libwebp
RUN yum -y install --enablerepo=remi gd-last
RUN yum -y install --enablerepo=remi-php70,remi php php-devel php-mbstring php-mysql php-pdo php-common php-gd

# 設定ファイルを上書き
COPY config/php.ini /etc/php.ini










