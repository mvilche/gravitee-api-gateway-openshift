FROM alpine:3.10

ENV GRAVITEE_VERSION=https://download.gravitee.io/graviteeio-apim/distributions/graviteeio-full-1.29.6.zip

RUN apk add --update --no-cache wget busybox-extras busybox-suid curl shadow openjdk11 unzip && \
mkdir -p /opt && cd tmp/ && echo "DESCARGANDO GRAVITEE..." && wget --no-verbose $GRAVITEE_VERSION -O /tmp/api.zip > /dev/null

RUN cd tmp/ && unzip api.zip && mv graviteeio-full*/graviteeio-gateway* /opt/gateway && \
rm -rf /tmp/*.zip /tmp/graviteeio* /etc/localtime

COPY run /usr/bin/run

RUN adduser -D -H -u 1001 api && usermod -aG 0 api && \
touch /etc/localtime /etc/timezone && \
chown -R 1001 /usr/bin/run /opt /etc/localtime /etc/timezone  && \
chgrp -R 0 /usr/bin/run /opt /etc/localtime /etc/timezone  && \
chmod -R g=u /usr/bin/run /opt /etc/localtime /etc/timezone

USER 1001

EXPOSE 8002

WORKDIR /opt/gateway

CMD ["/usr/bin/run"]
