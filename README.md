## Nginx
nginx web server

## To Start With
```sh
# install
brew install nginx

# access local nginx directory
cd /usr/local/etc/nginx/

# basic startup on port 8080( http://localhost:8080/ )
nginx

# various nginx terminologies( context and directives ) defined in:
vi /usr/local/etc/nginx/nginx.conf

# edit /usr/local/etc/nginx/nginx.conf and reload nginx( specify server root directive )
nginx -s reload

# include a mime.types file fix all the content-type issues
include mime.types;

# load balancer( Round-robin scheduling )
# forward user requests to different servers

# nginx config
http {
  # ...

  # available servers
  upstream backendserver {
    server 127.0.0.1:1111;
    server 127.0.0.1:2222;
    server 127.0.0.1:3333;
    server 127.0.0.1:4444;
  }

  server {
    listen 8080;
    root /Users/chen/go/src/github.com/tjcchen/nginx;

    # load balancer config
    location / {
      proxy_pass http://backendserver/;
    }
  }
}
```

## How To Configure Your TLS/SSl
```sh
# step1: create a ssl cert directory
sudo mkdir -p /usr/local/etc/nginx/ssl

# check openssl existence
openssl version

# step2: generate certs
# we generate a certificate( nginx.crt ) and private key( nginx.key ) under /usr/local/etc/nginx/ssl/ directory
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /usr/local/etc/nginx/ssl/nginx.key -out /usr/local/etc/nginx/ssl/nginx.crt

# step3: set your nginx config
server {
  listen 80 default_server;
  listen [::]:80 default_server;

  # SSL config
  listen 443 ssl default_server;
  listen [::]:443 ssl default_server;

  # SSL cert & key config
  ssl_certificate /usr/local/etc/nginx/ssl/nginx.crt;
  ssl_certificate_key /usr/local/etc/nginx/ssl/nginx.key;

  # ...
}

# step4: restart your server
sudo service nginx restart
nginx -s reload
```

## License
MIT
