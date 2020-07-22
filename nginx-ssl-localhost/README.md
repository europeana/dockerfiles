# NGINX SSL localhost

Deploy applications to Cloud Foundry.

NGINX on Debian with SSL key and 365 day certificate generated for localhost
when container is run.

SSL key and certificate are stored in /etc/nginx/ssl/, but NGINX is not
configured to use them. Downstream images are responsible for configuring
their server to use them, e.g. with:
```
server {
  listen 80;
  listen 443 ssl http2;
  server_name localhost;
  ssl_certificate /etc/nginx/ssl/server.crt;
  ssl_certificate_key /etc/nginx/ssl/server.key;
}
```
