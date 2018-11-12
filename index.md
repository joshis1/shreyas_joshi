---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: page
---
  <hr>
  <b> Welcome to my blogging channel. </b>
  

<img src="/assets/img/Home_Page.jpg" alt="Home Page">

Latest Blogs

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>

* [About](http://joshis1.github.io/about)
* [Code Download](http://joshis1.github.io/about)
