# NGINX配置备注

```conf
worker_processes  1;

events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;

    sendfile        on;

    keepalive_timeout  0;

    gzip on;
    gzip_min_length 1k;
    gzip_buffers 16 64k;
    gzip_http_version 1.1;
    gzip_comp_level 6;
    gzip_types text/plain application/x-javascript text/css application/xml;
    gzip_vary on;

    server {
        listen 80;
        server_name pre.xxxx.com;
        rewrite ^(.*) https://$server_name$1 permanent;
    }

    server {
        listen       443;
        server_name  pre.xxxx.com;

        ssl                         on;
        ssl_certificate             server.pem;
        ssl_certificate_key         server.key;
        ssl_session_timeout         5m;
        ssl_protocols               TLSv1 TLSv1.1 TLSv1.2;
        ssl_ciphers                 HIGH:!RC4:!MD5:!aNULL:!eNULL:!NULL:!DH:!EDH:!EXP:+MEDIUM;
        ssl_prefer_server_ciphers   on;

        location / {
            root /home/wwww;
            index index.html index.htm;
        }
    }

    server {
        listen       80;
        server_name  preapi.xxxx.com;
        rewrite ^(.*) https://$server_name$1 permanent;
    }

    server {
        listen       443;
        server_name  preapi.xxxx.com;

        ssl                         on;
        ssl_certificate             server.pem;
        ssl_certificate_key         server.key;
        ssl_session_timeout         5m;
        ssl_protocols               TLSv1 TLSv1.1 TLSv1.2;
        ssl_ciphers                 HIGH:!RC4:!MD5:!aNULL:!eNULL:!NULL:!DH:!EDH:!EXP:+MEDIUM;
        ssl_prefer_server_ciphers   on;

        location / {
            proxy_pass http://127.0.0.1:9999;
        }
    }
}
```