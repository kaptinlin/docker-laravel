FROM node:16-alpine as node
FROM nginx:1.20-alpine
SHELL ["/bin/ash", "-oeux", "pipefail", "-c"]

ENV TZ=UTC

RUN echo "http://mirrors.aliyun.com/alpine/v3.13/main/" > /etc/apk/repositories \
 && echo "http://mirrors.aliyun.com/alpine/v3.13/community/" >> /etc/apk/repositories

RUN apk update && \
  apk add --update --no-cache --virtual=.build-dependencies g++

# node command
COPY --from=node /usr/local/bin /usr/local/bin
# npm command
COPY --from=node /usr/local/lib /usr/local/lib
# yarn command
COPY --from=node /opt /opt
# nginx config file
COPY ./docker/nginx/*.conf /etc/nginx/conf.d/

WORKDIR /work/backend
