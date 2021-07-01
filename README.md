# nginx-config

## default config for example.com

```conf
server {
	listen 80;
	listen [::]:80;

	server_name example.com www.example.com;
	return 301 https://example.com$request_uri;
}

server {
	listen 443 ssl;
	listen [::]:443 ssl;

	server_name wexample.com;
	
	include snippets/platform.kz.ssl.conf;
	return 301 https://example.com$request_uri;
}	
server {
	listen 443 ssl;
	listen [::]:443 ssl;

	server_name example.com;
	
	include snippets/platform.kz.ssl.conf;
	
	location / {
    proxy_set_header Host $host;
    proxy_pass http://localhost:8080;
  }
}

```

## SSL snippet
```conf
ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem;
ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;

```
