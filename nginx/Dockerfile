FROM centos:6.8
MAINTAINER jiongJohn
ENV TIME_ZOME Asia/Shanghai
ARG NV="nginx-1.15.11"

ADD $NV.tar.gz /tmp
RUN yum install -y gcc gcc-c++ make openssl-devel pcre-devel \
    && mkdir -p /data/nginx \
    && mkdir -p /var/cache/nginx \
    && cd /tmp/$NV \
    &&  ./configure  --prefix=/data/nginx \
       --sbin-path=/usr/sbin/nginx \
       --modules-path=/usr/lib64/nginx/modules \
       --conf-path=/data/nginx/nginx.conf \
       --error-log-path=/var/log/nginx/error.log \
       --http-log-path=/var/log/nginx/access.log \
       --pid-path=/var/run/nginx.pid \
       --lock-path=/var/run/nginx.lock \
       --http-client-body-temp-path=/var/cache/nginx/client_temp \
       --http-proxy-temp-path=/var/cache/nginx/proxy_temp \
       --http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp \
       --http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp \
       --http-scgi-temp-path=/var/cache/nginx/scgi_temp \
       --user=nginx \
       --group=nginx \
       --with-compat \
       --with-file-aio \
       --with-threads \
       --with-http_addition_module \
       --with-http_auth_request_module \
       --with-http_dav_module \
       --with-http_flv_module \
       --with-http_gunzip_module \
       --with-http_gzip_static_module \
       --with-http_mp4_module \
       --with-http_random_index_module \
       --with-http_realip_module \
       --with-http_secure_link_module \
       --with-http_slice_module \
       --with-http_ssl_module \
       --with-http_stub_status_module \
       --with-http_sub_module \
       --with-http_v2_module \
       --with-mail \
       --with-mail_ssl_module \
       --with-stream \
       --with-stream_realip_module \
       --with-stream_ssl_module \
       --with-stream_ssl_preread_module \
       --with-cc-opt='-O2 -g -pipe -Wall -Wp,-D_FORTIFY_SOURCE=2 -fexceptions -fstack-protector --param=ssp-buffer-size=4 -m64 -mtune=generic -fPIC' \
       --with-ld-opt='-Wl,-z,relro -Wl,-z,now -pie' \
    && make \
    && make install \
    && echo "${TIME_ZOME}" > /etc/timezone \
    && mkdir /data/nginx/conf.d \
    && ln -sf /usr/share/zoneinfo/${TIME_ZOME} /etc/localtime \
    && rm -rf /tmp/nginx* \
    && yum clean all

WORKDIR /data/nginx/
EXPOSE 80
CMD ["/usr/sbin/nginx","-g","daemon off;"]