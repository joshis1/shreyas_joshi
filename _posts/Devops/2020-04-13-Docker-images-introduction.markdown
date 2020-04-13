---
layout: post
title:  "Docker-images-introduction"
date:   2020-04-13 14:56:31 + 1000
categories: Devops
---
This article is all about docker images. In this tutorial, we will learn on how to create a custom
docker image. This is just an introduction and doesn't cover the topic extensively.

**What is a docker image**  

Images are a key component when using docker. They provide the components and software necessary to run containers. They are built using a layered file system.
In short, it is a file containing the code and components needed to run software in a container. Docker containers and images use a layered file system. Each layer contains only the difference from the previous layer.

reference (https://docs.docker.com/v17.09/engine/userguide/storagedriver/imagesandcontainers/)

Example, the following will down an image from docker hub.

{% highlight ruby %}
 $docker image pull nginx
{% endhighlight %}

Containers and images use a layered file system. Each layer contains only the 
difference from the previous layer.

**Structure of image**  
An image consists of one or more read only layers.

**Strucutre of container**  
A container has one or more read only layers but in addition to it, it has a 
writeable layer. 

Example
{% highlight ruby %}
 Writeable container layer #Only container creates this layer
 Web-application - image  #read only layer
 Python - image  #read only layer
 Base Ubuntu OS image #read only layer
{% endhighlight %}

reference - (https://docs.docker.com/v17.09/engine/userguide/storagedriver/imagesandcontainers/)

**Advantages of layered file system**  
The layered file system allows multiple images and containers to share the same layer. Also, the image build time is reduced since we need to build the layers that have been changed in docker. This result in - 

{% highlight ruby %}
 1) smaller overall storage footprint
 2) faster image transfer 
 3) faster image build
{% endhighlight %}

For e.g. if you run five instances of container then each container share all the layers except writable container layer.  

**How to find what layers an image comprises of?**  
{% highlight ruby %}
 $docker image history <image name>
{% endhighlight %}

This will list the layers used to build an image.

**Components of a Dockerfile**  
**How to build your own docker image?**  
Docker hub provides a wide variety of useful public images. However, anyone 
running their own software using Docker needs to know how to create image themselves. The most common Dockerfile directives we should know. 

reference - (https://docs.docker.com/engine/reference/builder/)

{% highlight ruby %}
 $mkdir ~/custom-nginx
 $cd ~/custom-nginx
 $vi index.html
   Hello, World!
{% endhighlight %}

**What are directives in docker?**  
It is a set of instructions which are used to construct a docker image.
These instructions are called directives.

**Common Directives**  
{% highlight ruby %}
1) FROM - it starts a new build stage and sets the base image. It is usually must be the first directives in the Dockerfile(except ARG can be placed before FROM)  
2) ENV - sets environment variables. These can be referenced in the Dockerfile itself and are visible to the container at run time.  
3) RUN - it creates a new layer on top of the previous layer by running a command inside that new layer and committing the changes.  
4) CMD - specifically a default command used to run a container at execution time. 
{% endhighlight %} 

Now, create a docker file.

{% highlight ruby %}
  vi Dockerfile
# Simple nginx image
FROM ubuntu:bionic
ENV NGINX_VERSION 1.14.0-0ubuntu1.7
RUN apt-get update && apt-get install -y curl
RUN apt-get update && apt-get install -y nginx=$NGINX_VERSION
CMD ["nginx", "-g", "daemon off;"]
{% endhighlight %}

**Build and test the image**  
In order to build and test the image, we need to run the following.
{% highlight ruby %}
 $docker build -t custom-nginx .
 $docker run --name custom-nginx -d -p 8080:80 custom-nginx
curl localhost:8080
{% endhighlight %}

**More directives**  
Dockerfiles offer many different directives which we can use to build and customize our images.

1) EXPOSE - documents which port(s) are intended to published when running a container.
2) WORKDIR - sets the current working directory for subsequent directives such as 
ADD, COPY, CMD, ENTRYPOINT, etc. We can use relative path here too.
3) COPY - copy files from the local machine to the image.
4) ADD - it is similar to COPY, but can also pull files using a URL and extract an archive into loose files in the image.
5) STOPSIGNAL - specify the signal that will be used to stop the container.
6) HEALTHCHECK - specify a command to run in order to perform a custom health check to verify that the container is working properly.

Here is an example.
{% highlight ruby %}
 # Simple nginx image
FROM ubuntu:bionic
ENV NGINX_VERSION 1.14.0-0ubuntu1.7
RUN apt-get update && apt-get install -y curl
RUN apt-get update && apt-get install -y nginx=$NGINX_VERSION
WORKDIR /var/www/html/
ADD index.html ./
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
STOPSIGNAL SIGTERM
HEALTHCHECK CMD curl localhost:80
{% endhighlight %}

Now, rebuild the image and test it.
{% highlight ruby %}
 $docker build -t custom-nginx .
 $docker run -d -p 8080:80 custom-nginx
 $curl localhost:8080
{% endhighlight %}

Now, locate our running container with docker ps, then remove it to clean up the environment.
{% highlight ruby %}
 $docker ps
 $docker container rm -f <container id>
{% endhighlight %}

Here is a simple project that build docker image and runs the docker image.
[custom_docker_project](https://github.com/joshis1/docker_custom_build)

This brings an end to this article.