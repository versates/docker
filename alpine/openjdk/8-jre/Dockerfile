FROM alpine:3.4

MAINTAINER Versates <docker@versates.com>

RUN apk update && apk upgrade && \
    apk add openjdk8-jre && \
    rm -rf /var/cache/apk/*
