# Decommissioned site

NGINX Docker image which always responds with 200 static HTML content.

Intended to inform users about decommmisioned services.

Clients will receive an [HTML response](./usr/share/nginx/html/index.html).

For specific deployements additional text can be added to index.html on the running container.

For example, locally run:

```
docker exec decommissioned-site sed -i '14 i <p>Find additional information on <a href="https://www.europeana.eu">Europeana.eu</a>.</p>' usr/share/nginx/html/index.html
```
Or the contents of index.html could be overwritten entirely if larger changes should be required.

## Build

```sh
docker build -t europeana/decommissioned-site .
```

## Run

```sh
docker run -p 8080:80 -it --name decommissioned-site europeana/decommissioned
```
