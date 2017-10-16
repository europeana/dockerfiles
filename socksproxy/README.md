# Authenticated dante SOCKS proxy

Uses vimagick/dante image to supply a dante SOCKS proxy, but requires username
authentication.

Username is `socks` and password *must* be specified as the environment variable
`SOCKS_PASSWORD` passed to `docker run`:

```shell
docker run -p 1080:1080 -e SOCKS_PASSWORD=secret IMAGE
```
