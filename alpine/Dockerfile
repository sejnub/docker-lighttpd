FROM hypriot/rpi-alpine-scratch
MAINTAINER Daniel S.

RUN apk add --update lighttpd \
 && rm -rf /var/cache/apk/*

RUN mkdir -p /var/cache/lighttpd/compress/ \
 && chown -R lighttpd /var/cache/lighttpd/compress/

RUN apk add --update lighttpd       && \
    apk add --update jq             && \
    apk add --update openssh-client && \    
    apk add --update sshpass       

RUN rm -rf /var/cache/apk/*

EXPOSE 80

VOLUME /var/www/localhost

CMD ["lighttpd", "-D", "-f", "/etc/lighttpd/lighttpd.conf"]

######## The coming lines should be moved to lower line numbers as soon as they are stable

COPY alpine/conf/lighttpd.conf /etc/lighttpd
COPY alpine/conf/mod_cgi.conf  /etc/lighttpd
COPY var-www/html/*            /var/www/localhost/htdocs
COPY var-www/html/*            /var/www/localhost/htdocs


"$(pwd)"/var-www/html:/var/www/localhost/htdocs

RUN mkdir /var/www/localhost/cgi-bin

COPY alpine/cgi-bin/* /var/www/localhost/cgi-bin

