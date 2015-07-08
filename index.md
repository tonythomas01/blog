---
layout: page
title: Welcome to my Blog!
---
{% include JB/setup %}
## Introduce.Me()
    Name: Tony Thomas
    Gender: Male
    Language: Malayalam, English, PHP 
    Interests: Web Development, E-Mails
    E-mail : 01tonythomas [at] gmail [dot] com

--------------

## Latest Post 
<ul class="posts">
  {% for post in site.posts limit:1 %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>
      {{ post.content }}
    </li>
  {% endfor %}
</ul>

## Few Posts from the past
<ul class="posts">
  {% for post in site.posts limit:5 %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>
      {{ post.excerpt  }}
    </li>
  {% endfor %}
</ul>

## Note

I just moved my blog from [tttwrites.wordpress.com](http://tttwrites.wordpress.com) to here. So, ignore things for a while.


