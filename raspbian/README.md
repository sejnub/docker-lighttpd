# Info

# Build

````
cd ~
rm -rf docker-nginx
git clone https://github.com/sejnub/docker-nginx.git
cd ~/docker-nginx 
docker build -f raspbian/Dockerfile -t sejnub/nginx .
````


# Run

## Just to see if it starts
````
docker rm -f nginx; docker run -d -p 80:80 -p 443:443 --env-file /usr/local/etc/sejnub-credentials.env --name nginx sejnub/nginx
````

## Start interactively
````
docker rm -f nginx; docker run -it -p 80:80 -p 443:443 --env-file /usr/local/etc/sejnub-credentials.env --name nginx sejnub/nginx bash

nginx -g "daemon off;"

exit

````

## Attach

````
docker exec -it nginx /bin/bash
````

## xxxxx
````
docker rm -f nginx; docker run -d -p 80:80 -p 443:443 --env-file /usr/local/etc/sejnub-credentials.env --name nginx sejnub/nginx
````




eof
