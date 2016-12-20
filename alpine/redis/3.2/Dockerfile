FROM alpine:3.4

MAINTAINER Versates <docker@versates.com>

ENV LANG "en_US.UTF8"

RUN apk --update upgrade \
    && apk add redis \
    && rm -rf /var/cache/apk/*

VOLUME "/var/lib/redis"

EXPOSE 6379 16379

COPY entrypoint /usr/local/bin/
ENTRYPOINT [ "entrypoint" ]
CMD [ "redis-server" ]