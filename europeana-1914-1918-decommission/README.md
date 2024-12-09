# Europeana 1914-1918 Decommission

NGINX Docker image which always responds with 200 static HTML content.

Intended to inform users that the europeana 1914-1918 platform has been decommissioned and provide a link to the europeana.eu site.

Clients will receive an [HTML response](./usr/share/nginx/html/index.html).

## Build

```sh
docker build -t europeana/europeana-1914-1918-decommission .
```

## Run

```sh
docker run -p 8080:80 -it --name europeana-1914-1918-decommission europeana/europeana-1914-1918-decommission
```
