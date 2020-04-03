---
layout: post
title:  "Linux lighttpd"
date:   2020-04-03 14:23:31 +1300
categories: Utilities
---

This article is all about installing and running lighttpd.

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

Now, configure the root folder for lighttpd.

By default, the root folder is /var/www.
But, we will change the root folder here.

{% highlight ruby %}
#mkdir /home/httpd
#cp -Rv /var/www/* /home/httpd
#chown -R www-data /home/httpd
#chgrp -R www-data /home/httpd
{% endhighlight %}

Let's change the configuration now in lighttpd.conf

{% highlight ruby %}
#vi /etc/lighttpd/lighttpd.conf
server.document-root  "/home/httpd"
{% endhighlight %}

Enable, CGI in lighttpd.

{% highlight ruby %}

vi /etc/lighttpd/lighttpd.conf

#server.modules = (
    "mod_access",
    "mod_alias",
    "mod_compress",
    "mod_redirect",
    "mod_cgi",
    "mod_rewrite",
)

{% endhighlight %}

In order to get lighttd to recognize any python scripts we need to add
the following new section at the end of the file.

{% highlight ruby %}
$HTTP["url"] =~ "^/cgi-bin/" {
  cgi.assign = (".py" => "/usr/bin/python")
}
{% endhighlight %}

Give appropriate permission to the root folder.

{% highlight ruby %}
# chown www-data /home/httpd/cgi-bin
# chgrp www-data /home/httpd/cgi-bin
{% endhighlight %}

Now, write the hello.py

{% highlight ruby %}

vi /home/httpd/cgi-bin/hello.py

#! /usr/bin/python
#
print "Content-Type: text/html\n\n"
print '<html> <head> <meta-content="text/html; charset=UTF-8"/>'
print '<title> Raspberry  Pi </title> 
<p> 
for count in range(1,100)
print'Hello&nbspWorld...'
print "/p> <body> </html>
{% endhighlight %}

Finally, restart the lighttpd service.

{% highlight ruby %}
#service lighttpd restart
{% endhighlight %}

This brings an end to this article.