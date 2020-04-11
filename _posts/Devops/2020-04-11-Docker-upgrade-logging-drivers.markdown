---
layout: post
title:  "Docker-upgrade-logging-drivers"
date:   2020-04-11 17:23:31 +1300
categories: Devops
---
This article is all about downgrading and upgrading docker in Ubuntu. Also, 
we will cover logging drivers.

**Downgrade docker**
1. First stop the docker
2. remove the docker and don't purge it so that we don't docker containers.
3. Install the old docker version.
{% highlight ruby %}
 $sudo systemctl stop docker
 $sudo apt-get remove -y docker-ce docker-ce-cli 
 $sudo apt-get update
 $sudo apt-get install -y docker-ce=5:18.09.4~3-0~ubuntu-bionic docker-ce-cli=5:18.09.4~3-0~ubuntu-bionic
docker version
{% endhighlight %}

**Upgrade docker**
Here there is no need to remove the package or stop the docker.
{% highlight ruby %}
$sudo apt-get install -y docker-ce=5:18.09.5~3-0~ubuntu-bionic docker-ce-cli=5:18.09.5~3-0~ubuntu-bionic
$docker version
{% endhighlight %}

**Configuring logging drivers - splunk journald, etc**
This is a pluggable framework for accessing log data from services and containers in Docker. The storing and accessing container logs is an essential part of managing containers. Docker logging driver allow us
to choose our own logging implementation to fit our particular needs.

reference - (https://docs.docker.com/config/containers/logging/configure/)

First, check the current default logging driver. Next, edit 
daemon.josn to set a new default logging driver to either json-file or 
syslog.

{% highlight ruby %}
 $docker info | grep logging
 $sudo vi /etc/docker/daemon.json

{
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "15m"
  }
}
{% endhighlight %}
Next, restart docker after editing daemon.json

{% highlight ruby %}
 $sudo systemcl restart docker
{% endhighlight %}

If you run a docker container, overwrite the system default logging driver
settings for individual container.

{% highlight ruby %}
 $docker run --log-driver json-file --log-opt max-size=50m nginx
{% endhighlight %}

or syslog
{% highlight ruby %}
  $docker run --log-driver syslog nginx
{% endhighlight %}

This brings an end to this article.