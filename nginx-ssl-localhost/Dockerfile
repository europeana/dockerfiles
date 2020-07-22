FROM nginx:stable

RUN apt-get update && \
    apt-get -y install openssl && \
    rm -rf /var/lib/apt/lists/*

COPY localhost-ssl.sh /docker-entrypoint.d/90-localhost-ssl.sh
