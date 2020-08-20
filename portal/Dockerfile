FROM alpine:3.11

ENV GRAVITEE_VERSION=https://download.gravitee.io/graviteeio-apim/distributions/graviteeio-full-3.1.2.zip

RUN apk add --update --no-cache wget busybox-extras busybox-suid curl shadow apache2 unzip && \
sed -i -e "s/^Listen 80/Listen 8080/" /etc/apache2/httpd.conf && \
sed -ri -e 's!^(\s*ErrorLog)\s+\S+!\1 /proc/self/fd/2!g' /etc/apache2/httpd.conf && \
rm -rf /var/www/localhost/htdocs && \
wget --no-verbose $GRAVITEE_VERSION -O /tmp/api.zip > /dev/null

COPY run /usr/bin/run
RUN cd tmp/ && unzip api.zip && mv graviteeio-full*/graviteeio-portal-ui* /var/www/localhost/htdocs && \
rm -rf /tmp/*.zip && \ 
rm -rf  /etc/localtime && mkdir -p /opt/config && usermod -u 1001 apache && usermod -aG 0 apache && \
touch /etc/localtime /etc/timezone && \
chown -R 1001 /usr/bin/run /opt /var/www/localhost/htdocs /etc/apache2 /var/run/apache2 /usr/share/apache2 /var/log/apache2/ /etc/localtime /etc/timezone  && \
chgrp -R 0 /usr/bin/run /opt /var/www/localhost/htdocs /etc/apache2 /var/run/apache2 /usr/share/apache2 /var/log/apache2/ /etc/localtime /etc/timezone  && \
chmod -R g=u /usr/bin/run /opt /var/www/localhost/htdocs /etc/apache2 /var/run/apache2 /usr/share/apache2 /var/log/apache2/ /etc/localtime /etc/timezone

USER 1001

WORKDIR /var/www/localhost/htdocs

EXPOSE 8080

CMD ["/usr/bin/run"]