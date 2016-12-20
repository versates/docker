FROM alpine:3.4

MAINTAINER Versates <docker@versates.com>

ENV LANG "en_US.UTF8"

RUN apk --update upgrade \
    && apk add openjdk8-jre \
    && rm -rf /var/cache/apk/*