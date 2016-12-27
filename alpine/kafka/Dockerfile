FROM openjdk:8-jre-alpine

MAINTAINER Versates <docker@versates.com>

ENV SCALA_VERSION=2.11 \
    KAFKA_VERSION=0.10.1.1

WORKDIR "/var/lib/kafka"
VOLUME "/var/lib/kafka"

RUN addgroup -S kafka && adduser -h /var/lib/kafka -D -S -G kafka kafka \
    && apk add --update --no-cache wget su-exec \
    && wget -qO- "http://download.nextag.com/apache/kafka/${KAFKA_VERSION}/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz" | tar -xzf- \
    && mv "kafka_${SCALA_VERSION}-${KAFKA_VERSION}" /usr/local/kafka \
    && mkdir /var/log/kafka && mkdir /var/run/kafka \
    && chown -R kafka:kafka /var/lib/kafka /var/log/kafka /usr/local/kafka /var/run/kafka \
    && sed -i '/^#listeners=PLAINTEXT/s/^#//' /usr/local/kafka/config/server.properties \
    && sed -i 's/log.dirs=.*/log.dirs=\/var\/log\/kafka/' /usr/local/kafka/config/server.properties \
    && sed -i 's/dataDir=.*/dataDir=\/var\/lib\/kafka/' /usr/local/kafka/config/zookeeper.properties \
    && apk del --purge wget && rm -rf /var/cache/apk/*

EXPOSE 2181 9092

COPY entrypoint /usr/local/bin/
ENTRYPOINT ["entrypoint"]

COPY start-server /usr/local/bin/
COPY stop-server /usr/local/bin/
CMD ["start-server"]
