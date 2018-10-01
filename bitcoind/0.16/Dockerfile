FROM debian:stretch-slim

LABEL vendor="Versates, Inc" maintainer="docker@versates.com" version="1.0.0"

ENV LANG="en_US.UTF-8" \
    LANGUAGE="en_US.UTF-8" \
    LC_ALL="en_US.UTF-8" \
    LC_CTYPE="en_US.UTF-8" \
    PIDFILE="/var/run/bitcoin/bitcoind.pid" \
    TESTNET="true" \
    BITCOIN_DATA="/var/lib/bitcoin" \
    BITCOIN_VERSION="0.16.3" \
    DOWNLOAD_URL="https://bitcoin.org/bin" \
    DEBIAN_FRONTEND=noninteractive \
    DEBCONF_NONINTERACTIVE_SEEN=true

RUN apt-get update -q && \
    apt-get install -y -q locales-all locales && \
    apt-get install -y -q apt-utils gnupg curl && \
    addgroup --gid 321 --quiet --system bitcoin && \
    adduser --system --uid 321 --gid 321 --home "${BITCOIN_DATA}" --shell /bin/bash --quiet bitcoin && \
    mkdir /etc/bitcoin && \
    mkdir /var/run/bitcoin && \
    chown bitcoin:bitcoin /var/run/bitcoin && \
    cd /usr/src && \
    curl -sSLO "${DOWNLOAD_URL}/bitcoin-core-${BITCOIN_VERSION}/SHA256SUMS.asc" && \
    curl -SLO "${DOWNLOAD_URL}/bitcoin-core-${BITCOIN_VERSION}/bitcoin-${BITCOIN_VERSION}-x86_64-linux-gnu.tar.gz" && \
    curl -sSL https://bitcoin.org/laanwj-releases.asc | gpg -q --import && \
    gpg --verify SHA256SUMS.asc && \
    grep "bitcoin-${BITCOIN_VERSION}-x86_64-linux-gnu.tar.gz\$" SHA256SUMS.asc | sha256sum -c - && \
    tar xzf "bitcoin-${BITCOIN_VERSION}-x86_64-linux-gnu.tar.gz" && \
    install -m 0755 -o root -g root -t /usr/local/bin bitcoin-${BITCOIN_VERSION}/bin/* && \
    apt-get clean -q && \
    unset DEBIAN_FRONTEND DEBCONF_NONINTERACTIVE_SEEN DOWNLOAD_URL BITCOIN_VERSION && \
    rm -rf /usr/src/* && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /var/cache/apt/* && \
    rm -rf /var/tmp/* && \
    rm -rf /tmp/*

COPY entrypoint /usr/local/bin/
COPY bitcoin.conf /etc/bitcoin/

WORKDIR [ "/var/lib/bitcoin" ]
VOLUME [ "/var/lib/bitcoin", "/etc/bitcoin" ]

EXPOSE 8332 8333 18332 18333

USER bitcoin:bitcoin

ENTRYPOINT [ "entrypoint" ]

CMD [ "bitcoind", "-server", "-conf=/etc/bitcoin/bitcoin.conf" ]