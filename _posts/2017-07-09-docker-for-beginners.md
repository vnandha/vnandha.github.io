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

### Docker image commands

#### List docker images

{% highlight bash %}
docker images
{% endhighlight %}

#### List docker image with image sha

{% highlight bash %}
docker images --digests
{% endhighlight %}

#### pull an image

{% highlight bash %}
docker pull nginx
{% endhighlight %}

#### remove docker image

{% highlight bash %}
docker rmi <imageid>
{% endhighlight %}

### Docker run commands

#### Run a simple nginx container

{% highlight bash %}
docker run --name nginx-8080 -d  -p 8080:80 nginx

run: runs the image as container
--name name to the docker container
-d run in background
-p publish, portforward physical machines 8080 to the container port 80
{% endhighlight %}

#### Run another nginx container

{% highlight bash %}
docker run --name nginx-9080 -d  -p 9080:80 nginx
{% endhighlight %}

#### Run another variant to run in host network

{% highlight bash %}
docker run --name nginx-80 -d  --network=host nginx
{% endhighlight %}

#### Port binding issue

{% highlight bash %}
docker run --name nginx-80 -d  --network=host nginx #docker run disallow as the name is same
docker run --name nginx-81 -d  --network=host nginx #docker would start and see what happens
{% endhighlight %}

### Working with Running containers

#### List running containers

{% highlight bash %}
docker ps -a
{% endhighlight %}


#### Inspect a container

{% highlight bash %}
docker inspect <id>
{% endhighlight %}

#### Getting inside docker container

{% highlight bash %}
docker exec -it <id> bash
{% endhighlight %}

#### Run a container with interactive

{% highlight bash %}
docker run -i -t --rm=true --entrypoint=/bin/bash nginx

ip addr
ctrl+d
{% endhighlight %}

#### Run a container with interactive hostnetwork

{% highlight bash %}
docker run -i -t --rm=true --entrypoint=/bin/bash --network=host nginx

ip addr
ctrl+d
{% endhighlight %}

#### Execute a command directly

{% highlight bash %}
docker run  --rm=true nginx  uname -a
{% endhighlight %}

#### Mounting the directory as volumes inside the container

{% highlight bash %}
docker run  --rm=true nginx ls

mkdir /tmp/abcd; touch /tmp/abcd/xyz
docker run -v /tmp/abcd:/tmp/dockermount:ro  --rm=true nginx ls /tmp/dockermount
{% endhighlight %}
