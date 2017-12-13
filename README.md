# pihole_exporter

Containerised version of [pihole_exporter](https://github.com/nlamirault/pihole_exporter)

pihole_exporter is a Prometheus exporter for the Ad blocking DNS Server [PiHole](https://pi-hole.net)

Set the environmental variable of $PiHole as your PiHole Instance e.g http://10.0.0.53

---
#### 0.0.1 (2017-12-13)

Initial release

---
#### Example Run Command

```
docker run -d -p 9311:9331 -e PiHole="http://10.0.0.53" b3vis/pihole_exporter
```
---
#### Dockerfile
```
FROM golang:alpine AS build
MAINTAINER b3vis
RUN apk add git --no-cache && \
    go get github.com/nlamirault/pihole_exporter && \
    go install github.com/nlamirault/pihole_exporter

FROM alpine:latest
COPY --from=build /go/bin/pihole_exporter /go/bin/pihole_exporter
EXPOSE 9311
CMD /go/bin/pihole_exporter -pihole $PiHole
```
