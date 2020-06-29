FROM alpine:3.11

ENV ELASTIC_VERSION=https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-oss-7.8.0-no-jdk-linux-x86_64.tar.gz
ENV JAVA_HOME=/usr/lib/jvm/default-jvm

RUN apk add --update --no-cache wget busybox-extras bash busybox-suid curl shadow openjdk11 && \
wget --no-verbose $ELASTIC_VERSION -O /tmp/elastic.tar.gz > /dev/null && \
mkdir -p /opt/elasticsearch

RUN cd tmp/ && \
tar zxvf /tmp/elastic.tar.gz -C /opt/elasticsearch --strip-components 1 && \
rm -rf /tmp/*.tar.gz && \ 
rm -rf  /etc/localtime && \
touch /etc/localtime /etc/timezone

COPY run /usr/bin/run

RUN chown -R 1001 /usr/bin/run /opt && \
chgrp -R 0 /usr/bin/run /opt && \
chmod -R g=u /usr/bin/run /opt /etc/localtime /etc/timezone

USER 1001

WORKDIR /opt/elasticsearch

EXPOSE 9200 9300

CMD ["/usr/bin/run"]