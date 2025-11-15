FROM        golang:1.22.2-alpine3.19 AS base_image
RUN         apk add --update --no-cache -t build-deps curl gcc libc-dev libgcc
WORKDIR     /go/src/github.com/adnanh/webhook
COPY        ./webhook/webhook.version .
RUN         curl -#L -o webhook.tar.gz https://api.github.com/repos/adnanh/webhook/tarball/$(cat webhook.version) && \
  tar -xzf webhook.tar.gz --strip 1 && \
  go mod download && \
  go build -ldflags="-s -w" -o /usr/local/bin/webhook

FROM        alpine:3.17.0
RUN         apk add --update --no-cache curl tini tzdata git docker-cli docker-cli-compose
ENV         TZ=Asia/Shanghai
COPY        --from=base_image /usr/local/bin/webhook /usr/local/bin/webhook
WORKDIR     /config
EXPOSE      9000
ENTRYPOINT  ["/sbin/tini", "--", "/usr/local/bin/webhook"]
CMD         ["-verbose", "-hotreload", "-hooks=hooks.yml"]
