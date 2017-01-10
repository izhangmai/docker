#------------------------------------------------------------
#
#  用途: 胖纸囧开发测试环境
#  构成: Nginx-1.10.2
#
# @version    1.0
# @author     胖纸囧
# @email      757970599@qq.com
#

#------------------------------------------------------------
# FROM
FROM centos:7

#------------------------------------------------------------
MAINTAINER fatjiong 757970599@qq.com

#------------------------------------------------------------
# 基本软件安装
RUN yum -y install pcre pcre-devel zlib zlib-devel openssl openssl-devel libxml2 libxml2-devel libjpeg libjpeg-devel libpng libpng-devel curl curl-devel freetype freetype-devel libmcrypt libmcrypt-devel cmake gcc-c++ ncurses-devel perl-Data-Dumper autoconf wget libicu libicu-devel libmcrypt libmcrypt-devel vim

#------------------------------------------------------------
# 安装配置nginx
ENV NGINX="nginx-1.10.2"
#下载nginx安装包
#RUN cd /usr/local && wget http://nginx.org/download/$NGINX.tar.gz
COPY /$NGINX.tar.gz /usr/local
RUN cd /usr/local && tar vxzf $NGINX.tar.gz
RUN cd /usr/local/$NGINX && ./configure \
    --prefix=/usr/local/nginx \
    --conf-path=/etc/nginx/nginx.conf \
    --error-log-path=/var/log/nginx/error.log \
    --http-log-path=/var/log/nginx/access.log \
    --pid-path=/var/run/nginx.pid \
    --lock-path=/var/lock/nginx.lock \
    --user=nginx \
    --group=nginx \
    --with-http_ssl_module \
    --with-http_flv_module \
    --with-http_stub_status_module \
    --with-http_gzip_static_module \
    --http-client-body-temp-path=/tmp/nginx/client/ \
    --http-proxy-temp-path=/tmp/nginx/proxy/ \
    --http-fastcgi-temp-path=/tmp/nginx/fcgi/ \
    --with-pcre \
    --with-http_dav_module 
RUN cd /usr/local/$NGINX && make && make install
#------------------------------------------------------------
# 启动项设置
ADD /nginx /etc/init.d/nginx
RUN chmod +x /etc/init.d/nginx
RUN useradd nginx


#------------------------------------------------------------
# 暴露端口
EXPOSE 80

#------------------------------------------------------------
# 服务启动
CMD ["/etc/init.d/nginx start"]
