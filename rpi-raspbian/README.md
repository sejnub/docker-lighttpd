# Info

# Build

````
cd ~
rm -rf docker-lighttpd
git clone https://github.com/sejnub/docker-lighttpd.git
cd ~/docker-lighttpd 
docker build -f raspbian/Dockerfile -t sejnub/lighttpd .
````


# Run

## Just to see if it starts
````
docker rm -f lighttpd; docker run -d -p 80:80 -p 443:443 --env-file /usr/local/etc/sejnub-credentials.env --name lighttpd sejnub/lighttpd
````

## Start interactively
````
docker rm -f lighttpd; docker run -it -p 80:80 -p 443:443 --env-file /usr/local/etc/sejnub-credentials.env --name lighttpd sejnub/lighttpd bash

lighttpd -g "daemon off;"

exit

````

## Attach

````
docker exec -it lighttpd /bin/bash
````

## xxxxx
````
docker rm -f lighttpd; docker run -d -p 80:80 -p 443:443 --env-file /usr/local/etc/sejnub-credentials.env --name lighttpd sejnub/lighttpd
````




eof
