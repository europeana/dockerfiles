# Five Zero Three

NGINX Docker image which always responds with 503 Service (Temporarily)
Unavailable error.

The intended use is during planned maintenance of other services, whose
traffic would be routed to this service.

JSON clients, determined by Accept header or .json URL paths, will receive a
[JSON response](./usr/share/nginx/html/503.json); all other clients will receive
an [HTML response](./usr/share/nginx/html/503.html).

## Build

```sh
docker build -t europeana/five-zero-three .
```

## Run

```sh
docker run -p 8080:80 -it --name europeana-five-three-zero europeana/five-zero-three
```
