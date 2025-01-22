# Decommissioned site

NGINX Docker image which always responds with 410 static HTML content.

Intended to inform users about decommmisioned services.

Clients will receive an [HTML response](./usr/share/nginx/html/index.html). Which defaults to include the notice "This site has been decommissioned."

For specific deployements the notice text can be modified by setting an ENV value for `DECOMMISSION_NOTICE`.

Example:

```
ENV DECOMMISSION_NOTICE="This site has been decommissioned.</br>Find out more at <a href=\"https://www.europeana.eu\">Europeana.eu</a>."
```

Additionally the page title & heading can be modified by setting an ENV value for `DECOMMISSION_TITLE`.

Example:

```
ENV DECOMMISSION_TITLE="Decommissioned | website"
```

## Build

```sh
docker build -t europeana/decommissioned-site .
```

## Run

```sh
docker run -p 8080:80 -it --name decommissioned-site europeana/decommissioned-site
```
