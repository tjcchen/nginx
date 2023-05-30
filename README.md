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



```

## License
MIT
