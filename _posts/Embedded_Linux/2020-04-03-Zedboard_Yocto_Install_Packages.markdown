---
layout: post
title:  "Zedboard Yocto Install Packages"
date:   2020-04-03 18:13:31 +1300
categories: Embedded_Linux
---

This article is all about installing extra packages in Yocto build.
This is a very short article on how to install extra packages in Yocto.
For e.g, I would like to add curl and node js package in Yocto.

**Check whether those packages are already available or not**
The best thing is to check whether those packages already exist or not.
For e.g. run the command bitbake-layers show-recipes and redirect its output to a file.
Next, open your favourite editor and find the package. There is a good chance it is already
available and its the matter of compiling and installing that package to your root file system.

{% highlight ruby %}

$bitbake-layers show-recipes  > recipes.txt

{% endhighlight %}

Also, you can check using the following link -

[packages](http://layers.openembedded.org/layerindex/branch/warrior/layers/?)

**How to add those packages to your root file system**

First define in local.conf file what packages you would like to install.

{% highlight ruby %}
 
 WEB_PACKAGES = " \
  curl \
  nodejs \
"
{% endhighlight %}

Next append those packages.

{% highlight ruby %}
IMAGE_INSTALL_append = " ${WEB_PACKAGES}"
{% endhighlight %}


Now, build your image again.

{% highlight ruby %}
$bitbake core-image-minimal
{% endhighlight %}

Now, your root file system should have those packages - nodejs and curl.

This brings an end to this article.