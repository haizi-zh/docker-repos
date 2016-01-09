FROM ubuntu

MAINTAINER Haizi Zheng <haizi.zh@gmail.com>

#RUN apt-get update && apt-get -y upgrade && apt-get install -y gcc gcc-c++ make libtool zlib zlib-devel openssl openssl-devel pcre pcre-devel && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN apt-get update && apt-get -y upgrade && apt-get install -y build-essential

RUN apt-get install -y libpcre3-dev libssl-dev zlib1g-dev libtool

ADD nginx-1.8.0 /nginx-1.8.0
ADD nginx-goodies-nginx-sticky-module-ng /nginx-goodies-nginx-sticky-module-ng
ADD nginx_upstream_check_module-0.3.0 /nginx_upstream_check_module-0.3.0

RUN cd /nginx-1.8.0 && ./configure --prefix=/etc/nginx --sbin-path=/usr/sbin/nginx --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --pid-path=/var/run/nginx.pid --lock-path=/var/run/nginx.lock --http-client-body-temp-path=/var/cache/nginx/client_temp --http-proxy-temp-path=/var/cache/nginx/proxy_temp --http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp --http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp --http-scgi-temp-path=/var/cache/nginx/scgi_temp --with-http_ssl_module --with-http_realip_module --with-http_addition_module --with-http_sub_module --with-http_dav_module --with-http_flv_module --with-http_mp4_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_random_index_module --with-http_secure_link_module --with-http_stub_status_module --with-http_auth_request_module --with-threads --with-mail --with-mail_ssl_module --with-file-aio --with-http_spdy_module --with-cc-opt='-g -O2 -Wformat -Werror=format-security -Wp,-D_FORTIFY_SOURCE=2' --with-ld-opt='-Wl,-z,relro -Wl,--as-needed' --with-ipv6 --add-module=/nginx_upstream_check_module-0.3.0 --add-module=/nginx-goodies-nginx-sticky-module-ng && make && make install && mkdir -p /var/cache/nginx

RUN rm -rf /nginx-1.8.0 /nginx-goodies-nginx-sticky-module-ng /nginx_upstream_check_module-0.3.0

CMD []

ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]

EXPOSE 80 443

VOLUME ["/var/cache/nginx", "/var/log/nginx"]
