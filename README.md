This Docker image is **deprecated**.  Please use the [Heroku-16 image](https://hub.docker.com/r/heroku/heroku/).  
Learn more about [local development with Docker Compose](https://devcenter.heroku.com/articles/local-development-with-docker-compose) and [deploying your image to Heroku](https://devcenter.heroku.com/articles/container-registry-and-runtime). 

# [Heroku Go Docker image](https://hub.docker.com/r/heroku/go)

For use with the [heroku docker plugin](https://github.com/heroku/heroku-docker).

## Image tags

You can see all of the tags [here](https://hub.docker.com/r/heroku/go/tags/).

The `latest` tag will generally refer to the latest, possibly unsupported,
release of [Go](https://golang.org/dl), including betas and release candidates.

Once a final version is cut a separate tag will be used and updated.

## App.json

**Note: Please read the official documentation [here](https://devcenter.heroku.com/articles/docker)**.

To use this image with the heroku docker plugin add the following fields to your
application's `app.json` file:

```json
{
  "image": "heroku/go:<go version or latest>",
  "mount_dir": "src/<go package name; eg github.com/heroku-examples/go-websocket-chat-demo>",
}
```

Then run `heroku docker:init` in your application's directory. This will create
both  `Dockerfile` and `docker-compose.yml` files.

**Note on `mount_dir`**:  The go tooling requires that files be located inside
of `$GOPATH`. The heroku docker plugin and this docker image sets up a `$GOPATH`
 for you, but requires a little help from the developer to determine where to
 place your application. The correct value of mount_dir can be determined with
 the following command (requires [jq](https://stedolan.github.io/jq/)):

```term
$ jq -r '"src/" +.ImportPath' < ./Godeps/Godeps.json
```

### Example app.json

Source can be found [here](https://github.com/heroku-examples/go-websocket-chat-demo/blob/master/app.json).

```json
{
  "name": "Go Websocket Chat Demo",
  "description": "Go websocket chat demo application.",
  "keywords": [
    "streaming",
    "redis",
    "go"
  ],
  "image": "heroku/go:1.5",
  "mount_dir": "src/github.com/heroku-examples/go-websocket-chat-demo",
  "website": "http://github.com/heroku-examples/go-websocket-chat-demo",
  "repository": "http://github.com/heroku-examples/go-websocket-chat-demol",
  "scripts": {},
  "addons": [
    "heroku-redis"
  ]
}
```

## Slug Size

The images are large but the slugs created by `heroku docker:release` only
include your application's code, dependencies & compiled binaries so should be
relatively small.
