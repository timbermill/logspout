# Logspout with GELF adapter

This image contains [Logspout](https://github.com/gliderlabs/logspout) which is compiled with [GELF adapter](https://github.com/rickalm/logspout-gelf) and [Logstash adapter](https://github.com/looplab/logspout-logstash) so you can forward Docker logs as the Logspout command:

* in GELF format using `gelf://hostname:port`
* in Logstash format using `logstash://hostname:port`

## Usage

Always read the official instructions first. This image should work the same way. Just use `gelf` and/or `logstash` as the protocol scheme.

Remember to set the hostname of the container to something meaningfull, because that gets set as the source of the messages.

### CLI example

`docker run -d --name=logspout --restart=unless-stopped -h $(hostname -f) -v /var/run/docker.sock:/var/run/docker.sock vincit/logspout-gelf gelf://my.log.server:12201,logstash://my.log.server:5000`

### Docker Compose example

You could use this image with the following docker-compose file:

```
version: '2'

services:
  logspout:
    image: vincit/logspout-gelf
    hostname: my.message.source
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    command: gelf://my.log.server:12201,logstash://my.log.server:5000
    restart: unless-stopped
```

## Disclaimer

This image is provided as-is and only with best effort. We try to update this image with the latest Logspout stable version.
