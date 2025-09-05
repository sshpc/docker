FROM httpd:2.4

# 启用必要模块
RUN echo "LoadModule proxy_module modules/mod_proxy.so"            >> /usr/local/apache2/conf/httpd.conf && \
    echo "LoadModule proxy_fcgi_module modules/mod_proxy_fcgi.so"  >> /usr/local/apache2/conf/httpd.conf && \
    echo "LoadModule rewrite_module modules/mod_rewrite.so"        >> /usr/local/apache2/conf/httpd.conf

# 引入自定义虚拟主机配置
COPY vhost.conf /usr/local/apache2/conf/extra/vhost.conf
RUN echo "Include conf/extra/vhost.conf" >> /usr/local/apache2/conf/httpd.conf
