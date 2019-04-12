FROM centos:6.8
MAINTAINER jiongJohn
ENV TIME_ZOME Asia/Shanghai
ARG PV="php-5.5.17"
ARG PHPDIR="/usr/local/php"

ADD $PV.tar.gz /tmp
RUN yum install -y gcc gcc-c++ make gd-devel libxml2-devel libcurl-devel libjpeg-devel libpng-devel openssl-devel bison libxslt-devel \
    && cd /tmp/$PV \
    && ./configure --prefix=$PHPDIR \
       --with-curl \
       --with-freetype-dir \
       --with-gd \
       --with-gettext \
       --with-iconv-dir \
       --with-kerberos \
       --with-libdir=lib64 \
       --with-libxml-dir \
       --with-mysql \
       --with-mysqli \
       --with-openssl \
       --with-pcre-regex \
       --with-pdo-mysql \
       --with-pdo-sqlite \
       --with-pear \
       --with-png-dir \
       --with-xmlrpc \
       --with-xsl \
       --with-zlib \
       --enable-fpm \
       --enable-bcmath \
       --enable-libxml \
       --enable-inline-optimization \
       --enable-gd-native-ttf \
       --enable-mbregex \
       --enable-mbstring \
       --enable-pcntl \
       --enable-shmop \
       --enable-soap \
       --enable-sockets \
       --enable-sysvsem \
       --enable-xml \
       --enable-zip \
    && make \
    && make install \
    && cp $PHPDIR/etc/php-fpm.conf.default $PHPDIR/etc/php-fpm.conf \
    && sed -i '/;daemonize/a\daemonize = no' $PHPDIR/etc/php-fpm.conf \
    && sed -i 's/127.0.0.1/0.0.0.0/g' $PHPDIR/etc/php-fpm.conf \
    && echo "${TIME_ZOME}" > /etc/timezone \
    && ln -sf /usr/share/zoneinfo/${TIME_ZOME} /etc/localtime \
    && rm -rf /tmp/php* \
    && yum clean all

WORKDIR $PHPDIR
EXPOSE 9000
CMD ["sbin/php-fpm","-c","etc/php-fpm.conf"]
