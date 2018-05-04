# Nginx开启gzip

配置如下

```js
gzip  on;
gzip_min_length 1k;
gzip_buffers 4 16k;
gzip_http_version 1.0;
gzip_comp_level 5;
gzip_types text/plain application/javascript application/x-javascript text/javascript text/xml text/css;
gzip_disable "MSIE [1-6]\.";
gzip_vary on;
```