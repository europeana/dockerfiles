# Cloud Foundry blue-green deployment

FROM alpine:3

RUN mkdir /hooks && \
    apk add --no-cache -q bash curl jq grep && \
    curl -s -L "https://packages.cloudfoundry.org/stable?release=linux64-binary&version=v7&source=github" | tar -zx && \
    mv cf cf7 /usr/local/bin && \
    cf install-plugin app-autoscaler-plugin -f -r CF-Community

WORKDIR /deploy

ENV CF_API= \
    CF_APP_TYPE=buildpack \
    CF_USERNAME= \
    CF_PASSWORD= \
    CF_ORG= \
    CF_SPACE= \
    CF_STARTUP_TIMEOUT=120 \
    CF_ROUTES= \
    CF_APP_NAME=

COPY docker-entrypoint /

ENTRYPOINT ["/docker-entrypoint"]
CMD ["buildpack"]
