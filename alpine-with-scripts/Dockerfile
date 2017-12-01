FROM sejnub/lighttpd:rpi-alpine


# For unifi-tools/add-dns

RUN apk add --update bash           && \
    apk add --update jq             && \
    apk add --update openssh-client && \    
    apk add --update sshpass       



COPY var-www/cgi-bin/         /var/www/localhost/
RUN chown -R lighttpd         /var/www/localhost/cgi-bin/
RUN chmod -R ug+x             /var/www/localhost/cgi-bin/*




# eof
