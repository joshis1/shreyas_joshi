---
layout: post
title:  "Docker-basic-swarm-and-backup"
date:   2020-04-12 18:20:31 +1300
categories: Devops
---
This article is all about introduction to docker swarm. Also, finally we will talk about how to take 
backup.

**Introduction to docker swarm**
Docker swarm is a great way to get even more value
out of using containers. It allows for easily building
a distributed cluster where a container can be run
across multiple available servers. Thus, it can do 
orchestrating and scaling.

**What is orchestrating?**
The dictionary meaning is to plan or co-ordinate the
elements to produce a desired effect.

reference - 

(https://docs.docker.com/engine/swarm/key-concepts/)
(https://docs.docker.com/engine/swarm/swarm-tutorial/create-swarm/)

**What kind of nodes are there in swarm?**
In docker swarm, we have manager nodes and worker
nodes. Yes, there can be a cluster of managers and
a cluster of nodes. The worker nodes are the one
how runs the container. The manager node job is to 
delegate the work to worker nodes. The docker swarm
worker nodes handle the processing of workloads
in the swarm cluster. 

**How to setup Manager node in Docker Swarm?**
{% highlight ruby %}
  $docker swarm init --advertise-addr <ip address>
{% endhighlight %}

**How to check whether the container is manager or not?**
{% highlight ruby %}
 $$docker info
 or
 $docker node ls
{% endhighlight %}

**How to setup docker worker?**
In order to setup docker worker, first we need to 
run the following command on the manager node.
Here is the process of adding worker nodes to the swarm.

On docker manager node.
{% highlight ruby %}
  $docker swarm join-token worker 
{% endhighlight %}

The above command will return the command to run on the worker node. For e.g, the above command returned the following - 

docker swarm join --token SWMTKN-1-69wmtf5my5qg0znu9mkb6e3vxx7nq15ph1mmaxge5v0av9p1ve-7roxzv75ts0zve62v10czzno0 172.31.41.244:2377

Now, we should run the above command on the worker node.
{% highlight ruby %}
 cloud@worker1$ docker swarm join --token SWMTKN-1-69wmtf5my5qg0znu9mkb6e3vxx7nq15ph1mmaxge5v0av9p1ve-7roxzv75ts0zve62v10czzno0 172.31.41.244:2377
{% endhighlight %}

Since we ran this command, this node will join a swarm as a worker.

On worker run this command and you could Is Manager is
false.

{% highlight ruby %}
docker info | more
Swarm: active
 NodeID: 7ar25kulzn220rxebh6t5go56
 Is Manager: false
 Node Address: 172.31.35.210
 Manager Addresses:
  172.31.41.244:2377
{% endhighlight %}

Note you can run the below command only on the 
docker manager node and not on docker worker node.

{% highlight ruby %}
cloud@manager:~$ docker node ls
ID                            HOSTNAME            STATUS              AVAILABILITY        MANAGER STATUS      ENGINE VERSION
qgwdh5n4ovqfq9i8xof6q3lbx *   manager             Ready               Active              Leader              18.09.5
gca4t9bfionwdgl63dc5trbgn     worker1             Ready               Active                                  18.09.5
7ar25kulzn220rxebh6t5go56     worker2             Ready               Active   
{% endhighlight %}

reference - (https://docs.docker.com/engine/swarm/swarm-tutorial/add-nodes/)

**Docker swarm backup**
If you are managing a swarm cluster then it is important to be able to backup current swarm data 
and restore a previous backup. Here is the step
to take swarm backup.

Firstly, login to docker manager.

1) Stop the docker 
{% highlight ruby %}
  $sudo systemctl stop dockers
{% endhighlight %}

All the docker data is backed up in the following
location.
{% highlight ruby %}
 $/var/lib/docker/swarm/
{% endhighlight %}

Now, let's take the content of swarm and put it in the archive. Here the archive is called "backup.tar.gz"
{% highlight ruby %}
 $sudo tar -zcvf backup.tar.gz /var/lib/docker/swarm
{% endhighlight %}

Now, you can start the docker again.
{% highlight ruby %}
 $sudo systemctl start docker
{% endhighlight %}

**How to restore a previous backup?**

1) stop the docker
2) delete any existing files or directories under
/var/lib/docker/swarm/
3) extract the swarm backup to the location 
/var/lib/docker/swarm.
4) restart the docker.

Note, it is important to delete the existing files 
under /var/lib/docker/swarm/ otherwise there will be a conflict.
{% highlight ruby %}
 $sudo systemctl stop docker
 $sudo rm -rf /var/lib/docker/swarm/*
 $sudo tar -zxvf backup.tar.gz -C /var/lib/docker/swarm/
 $sudo systemctl start docker
{% endhighlight %}

**Docker internals - namespace and cgroups**
Namespaces and cgroups are Linux kernel features which docker uses in order to provide the basic functionality of running containers.

reference - 
(https://docs.docker.com/engine/docker-overview/#the-underlying-technology)
(https://docs.docker.com/engine/security/userns-remap/)

Namespaces are a Linux technology that allows processes to be isolated in terms of the resource they see. They can be used to prevent different processes from interfering or interacting with one 
another.

Docker uses namespaces to isolate containers.
It uses namespaces such as the following to isolate
resources for containers.

{% highlight ruby %}
1. pid - Process isolation
2. net -  network interfaces isolation
3. ipc - interprocess communication - Docker doesn't 
communicate with the process outside the container.
4. mnt - file system mounts - isolate the container like what file system mounts are available to it.
5. uts - kernel and version identifiers - like on what kernel it is working on and we can see limited things only.
{% endhighlight %}

**Control groups or cgroups**
The cgroups is for limiting resource usage.
A docker relies on linux technology cgroups. 
A cgroup limits an application to a specific set of 
resources. It enforce limits and constraints. For e.g.
memory available to a specific container.
In short, docker relies on kernel.

This brings an end to this article.