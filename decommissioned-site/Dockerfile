FROM nginx:stable-alpine

ENV NGINX_ENVSUBST_TEMPLATE_DIR=/usr/share/nginx/templates
ENV NGINX_ENVSUBST_OUTPUT_DIR=/usr/share/nginx/html
ENV DECOMMISSION_NOTICE="This site has been decommissioned."

COPY . /
