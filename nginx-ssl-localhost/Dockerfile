FROM nginx:stable

RUN apt-get update && \
    apt-get -y install openssl && \
    rm -rf /var/lib/apt/lists/* && \
    mkdir /etc/nginx/ssl

COPY localhost-ssl.sh /docker-entrypoint.d/90-localhost-ssl.sh
