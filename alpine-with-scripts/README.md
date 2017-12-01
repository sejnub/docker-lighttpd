# Thanks

This repository is based on [dastrasmue/rpi-lighttpd](https://github.com/dastrasmue/rpi-lighttpd). 
Thank you dastrasmue!

# TODO
- Make environment variables from env-file accessible tocgi script
  - https://redmine.lighttpd.net/projects/1/wiki/Docs_ModSetEnv


# Links


# Build

````

cd ~
rm -rf docker-lighttpd
git clone https://github.com/sejnub/docker-lighttpd.git


cd ~/docker-lighttpd
git clone https://github.com/sejnub/unifi-tools.git

mkdir ~/docker-lighttpd/var-www/cgi-bin/add-dns
cp ~/docker-lighttpd/unifi-tools/add-dns/* ~/docker-lighttpd/var-www/cgi-bin/add-dns



cd ~/docker-lighttpd 
docker build -f alpine-with-scripts/Dockerfile -t sejnub/lighttpd:rpi-alpine-with-scripts .


````


# Run

## Just to see if it starts
````
cd ~/docker-lighttpd 

docker rm -f lighttpd; docker run -d  -p 80:80 --env-file /usr/local/etc/sejnub-credentials.env --name lighttpd sejnub/lighttpd:rpi-alpine-with-scripts

````

## Start interactively
````
docker rm -f lighttpd; docker run -it -p 80:80 --env-file /usr/local/etc/sejnub-credentials.env --name lighttpd sejnub/lighttpd:rpi-alpine-with-scripts /bin/sh

lighttpd -D -f /etc/lighttpd/lighttpd.conf

````

## Attach

````
docker exec -it lighttpd /bin/sh

cd /var/www/localhost/cgi-bin/add-dns/
ls -al


tail -f /var/log/lighttpd/*

````

## Snippets
````
docker rm -f lighttpd; docker run -d -v "$(pwd)"/var-www/html:/var/www/localhost/htdocs -p 80:80 --env-file /usr/local/etc/sejnub-credentials.env --name lighttpd sejnub/lighttpd:rpi-alpine-with-scripts
````




eof
