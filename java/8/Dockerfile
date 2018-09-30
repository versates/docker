FROM debian:stretch-slim

MAINTAINER Versates <docker@versates.com>

ENV LANG en_US.utf8 \
    JAVA_INSTALLER="oracle-java8-installer" \
    JAVA_HOME="/usr/lib/jvm/java-8-oracle" \
    DEBIAN_FRONTEND=noninteractive DEBCONF_NONINTERACTIVE_SEEN=true

RUN apt update -q && apt upgrade -y -q && apt install -y -q gnupg locales \
    && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8 \
    && echo "${JAVA_INSTALLER}" shared/accepted-oracle-license-v1-1 select true | debconf-set-selections \
    && echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" \
        > /etc/apt/sources.list.d/webupd8team-java.list \
    && apt-key adv -q --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886 \
    && apt update -q \
    && apt install -y -q "${JAVA_INSTALLER}" \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /var/cache/apt/* \
    && rm -rf "/var/cache/${JAVA_INSTALLER}"

CMD [ "bash" ]
