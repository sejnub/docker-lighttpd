FROM sejnub/lighttpd:rpi-alpine


# For unifi-tools/add-dns

RUN apk add --update bash           && \
    apk add --update curl           && \
    apk add --update jq             && \
    apk add --update openssh-client && \    
    apk add --update sshpass        && \
    apk add --update nano       


RUN rm -rf /var/cache/apk/*


COPY var-www/cgi-bin/         /var/www/localhost/cgi-bin
RUN chown -R lighttpd         /var/www/localhost/cgi-bin/

RUN chmod    ugo-x            /var/www/localhost/cgi-bin/add-dns/*
RUN chmod    ug+x             /var/www/localhost/cgi-bin/add-dns/add-dns.sh /var/www/localhost/cgi-bin/add-dns/init.sh




# eof
