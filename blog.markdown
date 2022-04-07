---
layout: index
title: Blog
permalink: /blog/
---

<ul id="blogList">
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}" class="blogPosting"><span class="postDate">{{ post.date| date: "%d %B %Y" }} →</span> {{ post.title }}</a>
    </li>
  {% endfor %}
</ul>


<style type="text/css">
  #num1{
    color: #454545;
  }
</style>