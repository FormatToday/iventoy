# iventoy

A Docker image running [iventoy](https://www.iventoy.com/cn/index.html).

A github actions workflow runs daily to check if their is a new release.

<https://hub.docker.com/r/formattoday/iventoy>

## Docker Compose

This does not work with rootless Docker.  The container must be run as root.

```yaml
---
version: '3.9'
services:
  iventoy:
    image:formattoday/iventoy:latest
    container_name: iventoy
    restart: always
    privileged: true #must be true
    ports:
      - 26000:26000
      - 16000:16000
      - 10809:10809
      - 67-69:67-69/udp
    volumes:
      - ./app/isos:/app/iso
      - ./app/config:/app/data
      - ./app/log:/app/log
    environment:
      - AUTO_START_PXE=true # optional, true by default
```

Not necessary to expose all the listed ports.
<https://www.iventoy.com/cn/doc_portnum.html>
