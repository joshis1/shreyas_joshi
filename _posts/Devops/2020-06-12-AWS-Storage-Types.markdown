---
layout: post
title:  "AWS-Storage-Types-Brief"
date:   2020-06-12 16:23:31 +1300
categories: Devops
---

This article is all about different types of AWS Storage.  

**Types of AWS Storage**

There are total 5 types of storage.
Here are the storage types.

<img src="/assets/img/Storage_Types.png" alt="Storage Types">

**Simple Storage Service - S3 (object level storage)**
{% highlight ruby %}
a) You can access it anywhere. 
b) It is less costly.  
c) You can store objects only - like movie, database, music, pdf, anything. 
d) Inside S3 there are buckets. 
e) Unstructured data can be stored in S3. 
{% endhighlight %}

**Elastic File System - EFS**
This is useful in the scenario where we want to share the software or files.
For e.g. keep the software in the common space and share it via. VPC.
This can only be used by Linux based systems.


**Elastic Block Storage -EBS**
In EC2, the storage is block level storage.
You can access this storage only through EC2 and the EC2 should be attached to this storage.

**Glacier**
Its new name is S3 Glacier.
{% highlight ruby %}
a) This is cheaper storage compare to S3.
b) This is reliable, durable and highly available but cheap.
c) The latency to read this storage is high.
d) This is basically used for archiving and not used much.
e) This is not useful for daily purpose.
{% endhighlight %}

**Snowball**
A huge data cannot be migrated using internet. 
Basically, snowball is a device that is send to datacentre.
Data is collected in snow mall.

AWS offers a complete range of cloud storage services to support both application and 
archival compliance requirements. Select from object, file and block storage services as well
as cloud data migration options to start designing the foundation of your cloud IT environment.

This brings an end to this article.