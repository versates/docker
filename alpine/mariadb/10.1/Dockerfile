FROM alpine:3.4

MAINTAINER Versates <docker@versates.com>

ENV LANG="en_US.UTF8"

RUN addgroup -S mysql && adduser -h /var/lib/mysql -D -S -G mysql mysql \
    && apk --update upgrade \
    && apk add \
         pwgen \
         mariadb \
         mariadb-client \
    && rm -rf /var/cache/apk/* \
    && mkdir -p "/usr/local/docker/entrypoint/initdb.d" \
    && mkdir "/usr/local/docker/bin"

VOLUME "/var/lib/mysql"

EXPOSE 3306

COPY entrypoint "/usr/local/docker/bin/"
ENTRYPOINT [ "/usr/local/docker/bin/entrypoint" ]
CMD [ "/usr/bin/mysqld" ]