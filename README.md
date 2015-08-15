# Go Docker image

For use with the [heroku-docker](https://github.com/heroku/heroku-docker) cli plugin's compose branch.

app.json requirements ATM:

```json
{
  ...
  "image": "heroku/go:1.4.2",
  "mount_dir": "src/<go package name; eg github.com/heroku-examples/go-websocket-chat-demo>",
  ...
}
```
