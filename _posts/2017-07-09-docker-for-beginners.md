---
layout: default
title: Docker For Beginners
permalink: /blog/:year/:month/:day/:title/
---

## Concept

* Docker image is a package that contains your code, runtime and libraries.
* Container is runtime of the image.

## Install Docker

For MAC you could start with [Docker for Mac](https://www.docker.com/docker-mac)

## Docker commands walk through

### Docker image

* List docker images

{% highlight bash %}
docker images
{% endhighlight %}

* List docker image with image sha

```bash
docker images --digests```

# pull an image
docker pull nginx

# remove docker image
docker rmi <imageid>

# run a container
docker run --name nginx-8080 -d  -p 8080:80 nginx

run: runs the image as container
--name name to the docker container
-d run in background
-p publish, portforward physical machines 8080 to the container port 80

# run another one
docker run --name nginx-9080 -d  -p 9080:80 nginx

# run another variant; to run in host network
docker run --name nginx-80 -d  --network=host nginx

# run again
docker run --name nginx-80 -d  --network=host nginx #docker run disallow as the name is same
docker run --name nginx-81 -d  --network=host nginx #docker would start and see what happens


# list docker containers
docker ps -a

# inspect
docker inspect <id>

# getting inside docker container
docker exec -it <id> bash

# start docker with interactive
docker run -i -t --rm=true --entrypoint=/bin/bash nginx

ifconfig
ctrl+d

# start the docker with hostnetwork
docker run -i -t --rm=true --entrypoint=/bin/bash --network=host nginx

ifconfig
ctrl+d

# execute a command directly
docker run  --rm=true nginx  uname -a

# mounting the directory as volumes inside the docker you would see no such file or dir
docker run  --rm=true nginx ls

mkdir /tmp/abcd; touch /tmp/abcd/xyz
docker run -v /tmp/abcd:/tmp/dockermount:ro  --rm=true nginx ls /tmp/dockermount

# result in read only filesystem
