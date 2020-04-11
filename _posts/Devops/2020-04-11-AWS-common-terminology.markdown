---
layout: post
title:  "AWS-common-terminology"
date:   2020-04-11 16:23:31 +1300
categories: Devops
---
This article is all about some common terminologies used in AWS manual.
It is pretty important to know about these terms in order to understand AWS better.

**High Availability**
It is the availability of hardware, software and configuration
allowing a system to "recover quickly" in the event of a failure.
It is to minimize the downtime. 

**Fault tolerance**
The system designed to operate through a failure with no user impact.
This is more expensive and complex to achieve. In fault tolerance, 
there are no outages. Because of fault tolerance, customer won't have 
any impact. For e.g. load balancer managing - instance1, instance2 and
instance3. If instance1 fails then load balancer can switch to instance2.

We should customer what they want fault tolerance or high availability.

**Disaster recovery**
This is all about what are the important terms to understand during 
disaster recovery.

**Recovery point Objectives - RPO**

This is to tell how much a business can tolerate to lose, expressed 
in time. The maximum time between a failure and the last successful 
backup.

**Recovery time objectives - RTO**
The maximum amount of time a system can be down. 
This is all about how long a solution takes to recover from the point of
disaster to the point when the system starts running.

This comes down to a point like how much loss of time a business can tolerate.

In terms of cost, lowering the RPO increases the cost.
For e.g. taking backup every minute will increase cost.

Both RPO and RTO can be lowered but it needs cost. 

**What AWS supports**

AWS supports high availability.

**Scaling**

There are two types of scaling - vertical scaling and horizontal scaling.

**Vertical scaling**
Here we move from a single medium machine instance to large machine 
instance and finally x-large machine instance. By moving from medium
to large, we add cpu, memory, etc. Thus, the cost is increased drastically.
In case, we need to scale then a reboot is required since we need to add
more resources like RAM, CPU, etc.

**Horizontal scaling**

Here we add more instances. We add additional machines into a pool of
resources. This is pretty good and we don't have to reboot the machine.
Also, the cost can be minimized. However, in order to support horizontal scaling we need to write application in a way that it supports horizontal
scaling. This needs small servers and therefore less pricy. It spreads the
risk by shifting the load to different servers. Thus many times we can
scale without any service outages. For horizontal scaling, we should 
store the data centrally so that all instances can use it rather than
data stored at individual instance. This is more complicated but more
efficient.

**Three tier architecture**

{% highlight ruby %}
 1. Presentation
 2. logic
 3. data
{% endhighlight %}

If an application follows three tier architecutre then they 
can be scaled horizontally. Otherwise, they are called monolithic
application and therefore they can be scaled only vertically.

**Encryption**
It is a process used extensively in AWS. There are two types of
encryption - symmetrical and asymmetrical encryption.

The asymetrical encryption uses public and private keys. The
public and private keys are mathematically related to each other.
The private key is kept by the server whereas the public key is made
public i.e. used by applications in order to encrypt the data.
The server then uses its private key to decrypt the data.

Example of symmetric encryption using gpg.

{% highlight ruby %}
$echo "Hello Shreyas" > message.txt
$gpg -c message.txt
$cat message.txt.gpg
$echo RELOADAGENT | gpg-connect-agent
$gpg -o plain.txt message.txt.gpg
$cat plain.txt
{% endhighlight %}

Example of asymemtric encryption using gpg.

{% highlight ruby %}
 $gpg --gen-key
 $gpg --armor --output pubkey.txt --export 'shreyas'
 $gpg --armor --output privkey.asc --export-secret-keys 'shreyas'
 $gpg --encrypt --recipient 'shreyas' message.txt
 $gpg --output decrypted.txt --decrypt message.txt.gpg
{% endhighlight %}

**General architecture concepts**

1. Cost efficient or Cost effective architecture - Implement a solution within AWS using products or products features
that provide the required service for as little initial and ongoing 
cost as possible. This is about using your funds effectively and knowing
if product x is better or worse than product y for a given solution.  

2. Secure - In a systems architecture context, implementing a given solution that
secures data and operations as much as possible from an internal or 
external attack.

3. Application session state - Data that represents what a customer is 
doing, what they have chosen or what they have configured. Examples 
include items and quantities in a shopping cart. A session state can be
stored on a server called stateful server. If the session state is stored
externally then it called a stateless server.  

4. Undifferentiated heavy lifting - A part of an application, system
or platform that is not specific to your business. Allowing a vendor
AWS  to handle this part frees your staff to work on adding direct
value to your customers. Thus, we offload a day to day IT job to AWS.  

This brings an end to this article.