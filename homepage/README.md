# Homepage

## Using Socket Proxy
If you want to use socket proxy to use docker integrations, after starting `homepage` you need to edit it's config file the `docker.yaml` and need to set it up like this:

```
my-docker:
  host: socket-proxy
  port: 2375
```
