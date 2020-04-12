---
layout: post
title:  "AWS-accounting-region"
date:   2020-04-12 19:01:31 +1300
categories: Devops
---
This article talks about AWS accounts and AWS region.

**AWS accounts**
AWS accounts are more than just a way to log in and access AWS services. They are crucial AWS feature that AWS solutions architect can use to implement secure and high performance systems. 

**Capabilities of AWS accounting**

{% highlight ruby %}
1) Authentication
2) Authorization
3) Billing
{% endhighlight %}

**Authentication**
Login process - the analogy is that it is like a 
locked house. 

**Authorization**

AWS accounts are isolated. They are created initially
with a single root user. This user via its username/password/API keys, is the only identity that can use.
If the account credentials are leaked, the impact (blast radius) is limited to that account.

For e.g., the root user account 2 has no access to root user account 1. Authorization is controlled on a per account basis. The root user starts with full control of the account and its resources. Additional identities can be created or external identities can be granted access. Otherwise no identity except the  account root user has an access to resources.

**Billing**
Each account has billing information attached. 
Every AWS account has its own isolated billing information. This is initially in the form of an attached credit card, but established accounts can be
converted to use traditional, term-base invoicing.
By default, you are only billed for resources in your account. Billing or security exploits are limited to a single account. However, accounts can be linked and
configured to allow consolidated billing where a master account is charged for all member account resource usage.

**AWS regions**
This is nothing but a local grouping of infrastructure. Here the service is delivered from the region. The regions are isolated. If one region fails, then it won't affect others.

**Isolate data** - Let's say my data is in America then it will stay there only and it won't leave the region. All the regions are identified by region code.
There are certain services that can run globally - for e.g. S3 services run from global perspective. However, inside the S3, we are limited to a particular region. The AWS regions are connected with each other with a high speed network.

**AWS regions has availability zones**
A regions contains multiple availability zones, which are separated and isolated networks. A failure in one
availability zone generally won't impact another.
They are connected with redundant high speed low latency network connections.
You should run your services from multiple availability zones. Most AWS services run within 
availability zones. Some series operate from one Az,
while others replicate between AZs. Some services
allow you to choose the Az to use and some don't.
The availability zone can be utilized to do 
faul tolerance.

**VPC**
The VPC i.e. virtual private cloud is specific to a region. 

**Edge locations or Point of presence**
These are small pockets of AWS compute, storage and
networking close to major population and are generally used for edge computing and content delivery. They are not powerful region so we should minimize the services here. They have local storage and are connected to global AWS. They have low computing. 

As a solutions architect, one should pick a region that is close the customer otherwise the service will have latency.

**Tier Systems**
{% highlight ruby %}
 1. Point of Presence i.e. edge locations
 2. Availability zones
 3. AWS regions
{% endhighlight %}

references - 

Infrastructure website - 
(https://infrastructure.aws/)

(https://aws.amazon.com/about-aws/global-infrastructure/)

(https://docs.aws.amazon.com/general/latest/gr/rande.html)

This brings an end to this article.