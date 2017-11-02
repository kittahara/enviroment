#
# LAMP Base
#

FROM centos:6.7
MAINTAINER ktahara

# update yum
RUN yum update -y && yum clean all

# epel repo
RUN yum -y install epel-release.noarch epel-release && yum clean all
COPY epel.repo /etc/yum.repos.d/

# remi repo
RUN rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-6.rpm && yum clean all
COPY remi.repo /etc/yum.repos.d/

RUN rpm --rebuilddb; yum install -y yum-plugin-ovl

# set locale
RUN yum reinstall -y glibc-common && yum clean all
RUN localedef -f UTF-8 -i ja_JP ja_JP.UTF-8
ENV LANG ja_JP.UTF-8
ENV LANGUAGE ja_JP:ja
ENV LC_ALL ja_JP.UTF-8
RUN unlink /etc/localtime
RUN ln -s /usr/share/zoneinfo/Japan /etc/localtime

# :TODO 必要なものがあったらば追記。
# ===============================================================================================================
# BASE packages
# ===============================================================================================================
RUN yum --enablerepo=extras clean metadata
RUN yum install -y zlib zlib-devel make gcc gcc-c++ openssl openssl-devel readline-devel pcre pcre-devel
RUN yum install -y openssh openssh-server
RUN yum install -y net-tools wget sudo
RUN yum install -y tar zip unzip bzip2 which tree
RUN yum install -y git
