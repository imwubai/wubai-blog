# 在Nginx下配置使用单页面spa

配置如下

```js
server {
	listen  80;
	server_name ismumu.com;
	location / {
		try_files $uri $uri/ /index.html;
		root /www/dva-demo/dist;
	}
}
```