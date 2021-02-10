# Cloud Foundry blue-green deployment

FROM alpine:3

RUN apk -q update && \
    apk add -q bash curl jq grep && \
    curl -s -L "https://packages.cloudfoundry.org/stable?release=linux64-binary&version=v7&source=github" | tar -zx && \
    mv cf cf7 /usr/local/bin

WORKDIR /deploy

ENV CF_API= \
    CF_USERNAME= \
    CF_PASSWORD= \
    CF_ORG= \
    CF_SPACE= \
    CF_ROUTES= \
    CF_APP_NAME=

COPY docker-entrypoint /

ENTRYPOINT ["/docker-entrypoint"]
CMD ["deploy"]
