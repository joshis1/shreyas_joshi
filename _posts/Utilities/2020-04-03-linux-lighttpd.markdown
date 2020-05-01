---
layout: post
title:  "Linux lighttpd"
date:   2020-04-03 14:23:31 +1300
categories: Utilities
---

This article is all about installing and running lighttpd. We will configure lighttpd to 
support python CGI.

The lighttpd is nothing but a light weight web server.
It has a low memory foot print and it is quite useful in embedded systems.

The lighttpd has a dependency on the package gamin, the gamin package is used for file alteration monitoring.
Firstly, purge the lighttpd.

{% highlight ruby %}
#sudo apt remove --purge lighttpd
{% endhighlight %}

Next, install the gamin.

{% highlight ruby %}
#sudo apt-get install gamin
{% endhighlight %}

Afterwards, install the lighttpd again.

{% highlight ruby %}
sudo apt-get install lighttpd
{% endhighlight %}

Now, if you go your server ip then you will see the welcome page as shown below.

<img src="/assets/img/lighttpd_welcome_page.png" alt="lighttpd_welcome_page">

**Enabling Python CGI in lighttpd**  
Firstly, go to the lighttpd.conf file.

{% highlight ruby %}
#vim /etc/lighttpd/lighttpd.conf
{% endhighlight %}

Change the server docroot from 
{% highlight ruby %}
 server.document-root        = "/var/www/html"

 to

 server.document-root        = "/var/www/"

{% endhighlight %}

This way the cgi-bin can live inside /var/www/ folder.

Secondly, create the cgi-bin directory with root user-id and group.
{% highlight ruby %}
 #mkdir -p /var/www/cgi-bin/
{% endhighlight %}

**CGI program - python script**
Now, create your python script inside /var/www/cgi-bin/serverTime.py

{% highlight ruby %}
#! /usr/bin/python
#
import datetime

print "Content-Type: text/html\n\n"
print '<html> <head> <meta-content="text/html; charset=UTF-8"/>'
print '<title> lighttpd Simple Python </title><p>'
for count in range(1,100):
    x = datetime.datetime.now().time()
    print 'Current time is ' 
	print x
    print "</p> </body> </html>"
{% endhighlight %}

In the file system, we should see
{% highlight ruby %}
 # ls -l /var/www/cgi-bin/
total 4
-rw-r--r-- 1 root root 315 Apr 30 17:54 serverTime.py
{% endhighlight %}

Give executable permission to your python script.
{% highlight ruby %}

  # chmod 755 /var/www/cgi-bin/serverTime.py 
{% endhighlight %}

[Note] - In the python script, Shehbang is very necessary - #! /usr/bin/python otherwise it won't work.
You can check this reference for more understanding. 

[Shehbang](https://stackoverflow.com/questions/6908143/should-i-put-shebang-in-python-scripts-and-what-form-should-it-take)

I think the best way to debug lighttpd is by running the lighttpd daemon into foreground and using strace.
This way we get to know what is it doing and why is it failing.

{% highlight ruby %}
#strace lighttpd -D -f /etc/lighttpd/lighttpd.conf
{% endhighlight %}

Now, when I access the page, I see that this script is available as downloadable rather than running.

{% highlight ruby %}
  http://10.21.12.74/cgi-bin/serverTime.py
{% endhighlight %}

<img src="/assets/img/Python_script_as_downloadable.png" alt="Python_script_as_downloadable">

**What I am missing?**

oops, I missed to enable cgi as described in the home page of cgi.
I need to enable cgi mode in lighttpd by running the following command.

{% highlight ruby %}
#lighty-enable-mod cgi
{% endhighlight %}

Now, Run "service lighttpd force-reload" to enable changes

{% highlight ruby %}
#service lighttpd force-reload
{% endhighlight %}

Now, it is good and running. You can see its outcome.

<img src="/assets/img/ServerTime.png" alt="ServerTime">

This brings an end to this article.

[Reference](https://mike632t.wordpress.com/2013/09/21/installing-lighttpd-with-python-cgi-support/)