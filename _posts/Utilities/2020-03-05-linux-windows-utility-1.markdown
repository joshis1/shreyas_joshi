---
layout: post
title:  "Linux and Windows Utilities - Part 1"
date:   2020-03-05 14:23:31 +1300
categories: Utilities
---

This article is all about simple utitlities and to answer the simple questions being asked commonly.

**How to encrypt the password file?**

You could use openssl to encrypt the password file.
Here is the command provided by openssl to encrypt any file.

{% highlight ruby %}
$openssl aes-256-cbc  -e -k 'ABC' -in password.txt -out password_enc.txt
{% endhighlight %}

Now to read back,

{% highlight ruby %}
$openssl aes-256-cbc  -d -k 'ABC' -in password_enc.txt -out password_decrypted.txt
{% endhighlight %}

The AES stands for advanced encryption standard.
AES is advanced version than DES- Data Encryption Standard. It uses symmetric key algorithm, same key is used for both encryption and decryption.

Here 256 is the cipher key size.
The key size must be the multiple of 32 bits. CBC is the algorithm.
It stands for cipher block chaining. 

It is worth to note that the bigger the block size is, it takes more number of rounds to encrypt the data that means it is more secure.

In the above example 'ABC' is the key.
-e stands for encryption
-d stands for decryption

**How to delete the directory wih special names in linux?**

For file deletions, one trick is to wildcard as much of the name as you can, and use the -i (interactive) option to decide what subset of the matches to delete, one by one. The rmdir command does not have that, but the recursive file removal will deal with directories. E.g.

{% highlight ruby %}
$rm -r -i AB*20191217-163059*
{% endhighlight %}

**What is -exec keyword in linux command?**

'-exec' is an option specific to 'find' command. This is used to run other commands on the results returned from the 'find' command. So, exec doesn't exist by its own, it can be combined only with find command.

**Example**

{% highlight ruby %}
$find ./ -iname '*.c' -o -name '*.h' -o -name '*.l' -exec grep -in test1 /dev/null {} \;
{% endhighlight %}

The above can be simplified to

{% highlight ruby %}
find ./ -iname '*.[ch]' -exec grep -in test1 /dev/null {} \;
{% endhighlight %}

{% highlight ruby %}
{} expands to the filename of each file or directory found with find, this is uses as an argument to grep.
{% endhighlight %}

{% highlight ruby %}
; - ends the command executed by exec. Escape by '\' so that ';' is not used by the shell but it is used by find.
{% endhighlight %}

Because ';' is a valid command in shell linux. For e.g.

{% highlight ruby %}
$cat password.txt; cat password_enc.txt  
{% endhighlight %}

The above will display password.txt and then it will display password_enc.txt. 

In our case, we don't want to use ';' by shell but to pass this to exec. So that's why we are using escape character '\'.

**What is the utility in Windows to run DHCP Server for tftp purpose?**

Here is the utility that I use in Windows10 to run my DHCP server.

[dhcp server](https://www.dhcpserver.de/cms/)

**What is the utility to see what IP addresses have been assigned by the DHCP Server**

This utility nmap is very powerful and can be useful even to know what are the different IP addresses  that 
are active. 

{% highlight ruby %}

$sudo nmap -sP 11.11.11.1-254

Starting Nmap 7.40 ( https://nmap.org ) at 2020-03-29 22:59 PDT
Nmap scan report for 11.11.11.1
Host is up (-0.099s latency).
MAC Address: 00:1B:21:A7:62:44 (Intel Corporate)
Nmap scan report for 11.11.11.4
Host is up (0.00069s latency).
MAC Address: 78:45:01:05:98:40 (Unknown)
Nmap scan report for 11.11.11.3
Host is up.
Nmap done: 254 IP addresses (3 hosts up) scanned in 15.42 seconds 
{% endhighlight %}



This brings an end to this article. This article was just to touch some
common commands and utilities to address common problems or tasks.