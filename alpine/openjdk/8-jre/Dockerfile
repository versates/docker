FROM alpine:3.4

MAINTAINER Versates <docker@versates.com>

ENV LANG en_US.utf8

RUN apk update -q --no-progress && apk upgrade -q --no-progress && \
    apk add -q --no-progress openjdk8-jre && \
    rm -rf /var/cache/apk/*
