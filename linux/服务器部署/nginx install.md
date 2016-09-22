#!/usr/bin/env bash

yum install -y subversion
yum install -y flex bison
yum install -y git
yum install -y gcc gcc-c++ autoconf automake
yum install -y zlib zlib-devel openssl openssl-devel pcre-devel
yum install -y libxml*
yum install -y openssl
yum install -y openssl-devel
yum install gcc zlib-devel xz openssl-devel bzip2 bzip2-devel lrzsz -y
yum install libjpeg-turbo-devel -y
yum install zlib-devel -y
yum install libjpeg-turbo-devel -y


mkdir -p /home/wwww
mkdir -p /home/admin/logs/nginx/

cd nginx/nginx-1.9.10

./configure --prefix=/usr/local/nginx \
--sbin-path=/usr/sbin/nginx \
--error-log-path=/home/admin/logs/nginx/error.log \
--with-http_ssl_module \
--with-http_flv_module \
--with-http_gzip_static_module \
--http-log-path=/home/admin/logs/nginx/access.log \
--with-http_stub_status_module \
--with-stream \
--with-http_slice_module

make && make install

echo "nginx" >> /home/wwww/index.html
nginx