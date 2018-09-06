FROM nginx

MAINTAINER Europeana Foundation <development@europeana.eu>

ENV DEBIAN_FRONTEND noninteractive

WORKDIR /data

RUN apt-get update
RUN apt-get -yq install curl gnupg2
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get -yq install gcc make php ruby ruby-dev nodejs

RUN echo "gem: --no-rdoc --no-ri" >> /etc/gemrc
RUN gem install compass

COPY ./cors.conf /etc/nginx/cors.conf
COPY ./default.conf /etc/nginx/conf.d/default.conf
