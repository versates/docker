FROM debian:stretch-slim

LABEL vendor="Versates, Inc" maintainer="Ramses Vidor (@ramsvidor)" version="1.0.0"

ENV LANG="en_US.UTF-8" \
    LANGUAGE="en_US.UTF-8" \
    LC_ALL="en_US.UTF-8" \
    LC_CTYPE="en_US.UTF-8" \
    DEBIAN_FRONTEND=noninteractive \
    DEBCONF_NONINTERACTIVE_SEEN=true

RUN apt-get update -q && \
    apt-get install -y -q locales-all locales && \
    apt-get install -y -q apt-utils gnupg curl build-essential && \
    curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
    apt-get update -q && \
    apt-get install -y nodejs && \
    npm install -g --no-optional blockchain-wallet-service && \
    apt-get clean -q && \
    unset DEBIAN_FRONTEND DEBCONF_NONINTERACTIVE_SEEN && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /var/cache/apt/* && \
    rm -rf /var/tmp/* && \
    rm -rf /tmp/*

EXPOSE 3000

CMD [ "blockchain-wallet-service", "start", "--port", "3000" ]
