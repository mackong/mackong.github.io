---
layout: page
title: MacKong -- 个人博客
header: MacKong -- 个人博客
---
{% include JB/setup %}

<ul class="posts">
  {% for post in site.posts %}
    <li>
		<h3 class="title"><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a><span class="date">{{ post.date | date_to_string }}</span></h3>
		<p class="excerpt">{{ post.excerpt }}</p>
	</li>
  {% endfor %}
</ul>
