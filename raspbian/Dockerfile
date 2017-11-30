FROM tobi312/rpi-nginx



# For unifi-tools/add-dns

RUN apt-get update                          && \
    apt-get install -yqq jq                 && \
    apt-get install -yqq git                && \
    apt-get install -yqq openssh-client     && \
    apt-get install -yqq sshpass

RUN git clone https://github.com/sejnub/unifi-tools.git && \
    mkdir /usr/share/add-dns                            && \
    cp -r unifi-tools/add-dns /usr/share                && \
    rm -rf unifi-tools                                  && \    
    cd /usr/share/add-dns                               && \
    . ./init.sh                           

COPY var-www/html/*.html /var/www/html

# cd /usr/share/add-dns; ./add-dns.sh

# CMD ["nginx", "-g", "daemon off;"]
