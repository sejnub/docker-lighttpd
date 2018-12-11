# Thanks

This repository is based on [dastrasmue/rpi-lighttpd](https://github.com/dastrasmue/rpi-lighttpd). 
Thank you dastrasmue!

## TODO
- Make environment variables from env-file accessible to the cgi script

  - https://redmine.lighttpd.net/projects/1/wiki/Docs_ModSetEnv

- looks like here we have to set the executable flag to the filed in cgi-bin again
- Idea: In cgi-bin are only executables, if an executable needs additional files (like add-dns) these are in one subdirectory per executable (or maybe some similar executables which need the same resources

## Build and run detached

- First you have to build sejnub/lighttpd:rpi-alpine. Do it as describe at <https://github.com/sejnub/docker-lighttpd/tree/master/rpi-alpine>

- Now execute the following

````
## Precondition: The imaga sejnub/lighttpd:rpi-alpine exists.

## Build


cd ~
rm -rf docker-lighttpd
git clone https://github.com/sejnub/docker-lighttpd.git


cd ~/docker-lighttpd
git clone https://github.com/sejnub/unifi-tools.git

mkdir ~/docker-lighttpd/var-www/cgi-bin/add-dns
cp ~/docker-lighttpd/unifi-tools/add-dns/* ~/docker-lighttpd/var-www/cgi-bin/add-dns


cd ~/docker-lighttpd 
docker build -f rpi-alpine-with-scripts/Dockerfile -t sejnub/lighttpd:rpi-alpine-with-scripts .

## Start detached

cd ~/docker-lighttpd 

docker rm -f lighttpd; docker run -d  --restart always -p 80:80 --env-file /usr/local/etc/sejnub-credentials.env -v /usr/local/etc/sejnub-credentials.env:/usr/local/etc/credentials.env --name lighttpd sejnub/lighttpd:rpi-alpine-with-scripts

````


## Start interactively
````
docker rm -f lighttpd; docker run -it -p 80:80 --env-file /usr/local/etc/sejnub-credentials.env -v /usr/local/etc/sejnub-credentials.env:/usr/local/etc/credentials.env --name lighttpd sejnub/lighttpd:rpi-alpine-with-scripts /bin/sh

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
