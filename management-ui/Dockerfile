FROM alpine:3.11

RUN apk add --update --no-cache wget busybox-extras busybox-suid curl shadow apache2 unzip && \
sed -i -e "s/^Listen 80/Listen 8080/" /etc/apache2/httpd.conf && \
sed -ri -e 's!^(\s*ErrorLog)\s+\S+!\1 /proc/self/fd/2!g' /etc/apache2/httpd.conf && \
rm -rf /var/www/localhost/htdocs

COPY run /usr/bin/run
COPY graviteeio-management-ui-1.30.5 /var/www/localhost/htdocs
RUN rm -rf  /etc/localtime && mkdir -p /opt/config && usermod -u 1001 apache && usermod -aG 0 apache && \
touch /etc/localtime /etc/timezone && \
chown -R 1001 /usr/bin/run /opt /var/www/localhost/htdocs /etc/apache2 /var/run/apache2 /usr/share/apache2 /var/log/apache2/ /etc/localtime /etc/timezone  && \
chgrp -R 0 /usr/bin/run /opt /var/www/localhost/htdocs /etc/apache2 /var/run/apache2 /usr/share/apache2 /var/log/apache2/ /etc/localtime /etc/timezone  && \
chmod -R g=u /usr/bin/run /opt /var/www/localhost/htdocs /etc/apache2 /var/run/apache2 /usr/share/apache2 /var/log/apache2/ /etc/localtime /etc/timezone

USER 1001

EXPOSE 8080

CMD ["/usr/bin/run"]
