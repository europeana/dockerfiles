# Cloud Foundry (CF) blue-green deployment

Makes blue-green app deployments on Cloud Foundry.

## Usage

### Build or pull

#### Build from source

```
docker build -t europeana/cf-blue-green-deploy .
```

#### Pull from Docker Hub

```
docker pull europeana/cf-blue-green-deploy
```

### Configure

Configuration of Cloud Foundry settings is by environment variable on the
Docker container. All are **required** at run time.

* `CF_API`: API endpoint
* `CF_USERNAME`: username
* `CF_PASSWORD`: password
* `CF_ORG`: org
* `CF_SPACE`: space
* `CF_DOMAIN`: route domain
* `CF_HOSTNAME`: route hostname
* `CF_APP_NAME`: app name, to which the `-blue` or `-green` suffix will be added

It is suggested to copy the supplied [.env.example](./.env.example) to .env,
populate for your CF provider and app, and pass to Docker when running the
image, with `--env-file .env`. All following examples assume such configuration.

### Run

#### `cf push` arguments

No arguments are set by default on the `cf push` command, but should instead
be supplied as the `docker run` command.

For example:
```
docker run --env-file .env \
           europeana/cf-blue-green-deploy \
           -f manifest.yml --vars-file vars.yml
```

This is equivalent to running: `cf push ${BLUE_GREEN_APP_NAME} -f manifest.yml --vars-file vars.yml`

#### With a manifest & local data

If the app needs to push local data (which will generally be the case unless using
a Docker image), then mount the local data directory into the container as
`/deploy`.

For example:
```
docker run --env-file .env --mount type=bind,source=/path/to/app,target=/deploy \
           europeana/cf-blue-green-deploy \
           -f manifest.yml
```

#### With a Docker image

For example:
```
docker run --env-file .env \
       europeana/cf-blue-green-deploy \
       --docker-image nginx -m 32M
```


## How it works

This blue-green deployment agent operates based on routing. It is given a
single primary route for the application, and whichever colour is presently
mapped to that route is the active one.

The other colour will be deployed with the code changes, then the route remapped
to point to it.

### Example

1. Given an app named `myapp`, a domain `example.org` and a hostname `www`, the
  [entrypoint](./docker-entrypoint) will use the CF CLI to look for the route
  `www.example.org`, then:
    * If one exists, and the first mapped app is named `myapp-blue`, then the blue
      colour is active and green will be deployed; vice versa if it is named `myapp-green`.
    * If one exists but the first mapped app is not named either `myapp-blue` or
      `myapp-green` then it will exit.
    * If one does not exist, this is assumed to be the first deployment and blue
      will be deployed.
2. The new colour is pushed as `myapp-blue` or `myapp-green`
3. The route `www.example.org` is mapped to the new colour
4. The route `www.example.org` is unmapped from the old colour (if there is one)
5. The old colour is stopped (if there is one)


## License

See [LICENSE.md](../LICENSE.md).
