FROM alpine:3.4

MAINTAINER Versates <docker@versates.com>

RUN apk update && apk upgrade \
    && apk add bash openssh \
    && rm -rf /var/cache/apk/*

RUN mkdir -p ~root/.ssh && chmod 700 ~root/.ssh \
    && echo -e "Port 22\n" >> /etc/ssh/sshd_config \
    && cp -a /etc/ssh /etc/ssh.cache

EXPOSE 22

COPY entrypoint /usr/local/bin/
ENTRYPOINT [ "entrypoint" ]
CMD [ "/usr/sbin/sshd", "-D", "-f", "/etc/ssh/sshd_config" ]