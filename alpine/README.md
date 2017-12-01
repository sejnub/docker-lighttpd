# Thanks

This repository is based on [dastrasmue/rpi-lighttpd](https://github.com/dastrasmue/rpi-lighttpd). 
Thank you dastrasmue!

# TODO

- Currently the logs are not forwarded to docker like they should be. Fix that!
  - https://redmine.lighttpd.net/issues/2731
- Make mod_cgi work!
  - https://redmine.lighttpd.net/projects/1/wiki/docs_modcgi


# Build

````
cd ~
rm -rf docker-lighttpd
git clone https://github.com/sejnub/docker-lighttpd.git
cd ~/docker-lighttpd 
docker build -f alpine/Dockerfile -t sejnub/lighttpd .
````


# Run

## Just to see if it starts
````
cd ~/docker-lighttpd 

docker rm -f lighttpd; docker run -d -p 80:80 --env-file /usr/local/etc/sejnub-credentials.env --name lighttpd sejnub/lighttpd

docker rm -f lighttpd; docker run -d -v "$(pwd)"/var-www/html:/var/www/localhost/htdocs -v "$(pwd)"/alpine/conf:/etc/lighttpd -p 80:80 --env-file /usr/local/etc/sejnub-credentials.env --name lighttpd sejnub/lighttpd

````

## Start interactively
````
docker rm -f lighttpd; docker run -it -v "$(pwd)"/var-www/html:/var/www/localhost/htdocs -v "$(pwd)"/alpine/conf:/etc/lighttpd -p 80:80 --env-file /usr/local/etc/sejnub-credentials.env --name lighttpd sejnub/lighttpd /bin/sh

lighttpd -D -f /etc/lighttpd/lighttpd.conf

````

## Attach

````
docker exec -it lighttpd /bin/sh

````

## xxxxx
````
docker rm -f lighttpd; docker run -d -p 80:80 -p 443:443 --env-file /usr/local/etc/sejnub-credentials.env --name lighttpd sejnub/lighttpd

````




eof
