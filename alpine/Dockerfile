FROM hypriot/alpine
MAINTAINER Daniel S.

RUN apk add --update lighttpd \
 && rm -rf /var/cache/apk/*

# HB: Enable this later, when starting to use compress
# RUN mkdir -p /var/cache/lighttpd/compress/ \
#  && chown -R lighttpd /var/cache/lighttpd/compress/


RUN apk add --update lighttpd    

RUN rm -rf /var/cache/apk/*

EXPOSE 80

# VOLUME /var/www/localhost

CMD ["lighttpd", "-D", "-f", "/etc/lighttpd/lighttpd.conf"]

######## The coming lines should be moved to lower line numbers as soon as they are stable

RUN mkdir /var/www/localhost/cgi-bin

COPY alpine/conf/lighttpd.conf /etc/lighttpd
COPY alpine/conf/mod_cgi.conf  /etc/lighttpd
RUN chown -R lighttpd          /etc/lighttpd

COPY var-www/html/*            /var/www/localhost/htdocs/
RUN chown -R lighttpd          /var/www/localhost/htdocs/

COPY var-www/cgi-bin/*         /var/www/localhost/cgi-bin/
RUN chown -R lighttpd          /var/www/localhost/cgi-bin/
RUN chmod ug+x                 /var/www/localhost/cgi-bin/*



