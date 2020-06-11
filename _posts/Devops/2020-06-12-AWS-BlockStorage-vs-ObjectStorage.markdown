---
layout: post
title:  "AWS-Block-Storage-vs-ObjectStorage"
date:   2020-06-12 16:23:31 +1300
categories: Devops
---

This article is all about Block Storage vs. Object Storage.

**Block Storage vs. Object Storage**

S3 is object storage whereas EBS is block storage.

**EBS block storage**

Block storage is suitable for transactional database, random read/write loads and
structured database storage. For parallel processing, we use block storage.

Block storage divides the data to be stored in evenly sized blocks (data chunk) for instance, 
a file can be split into evenly sized blocks before it is stored.
For e.g., Data is 5Mb, it will be stored in evenly block size i.e. equal block size.
They do indexing i.e. for each each block so that retrieving is possible.
Data blocks stored in evenly sized blocks (data chunks). For instance, a file can be split 
into evenly sized blocks before it is stored. Data blocks stored in block storage would not contain
meta data ( data like created, modified, content type, etc). Block storage only keeps the address(index)
where the datablocks are stored, it does not care what is in that block, just how to retrieve it when
required. Block storage can only be accessed through EC2 ie. instance.

Example - EBS, Elastic block storage. Just like C drive, D drive, e drive it will be mounted with EC2 
instance.

**Object Storage**
Object stores the file as a whole and does not divide them. 
In object storage, an object is the file/data itself, its metadata. 
The object will have a global unique id. The object global unique id, is a unique identifier 
for the object ( can be the object name itself) and it must be unique such that it can be retrieved 
disregarding  where its physical storage location is. Object storage cannot be mounted as a drive.

Example of object storage solutions - Dropbox, AWS S3.
They can be accessed through internet i.e. through http or https - we can access S3.

This brings an end to this article.
