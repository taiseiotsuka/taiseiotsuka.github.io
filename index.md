---
layout: default
title: とあるルビイストの備忘録
lang: ja_JP
---

<div>
{% for post in site.posts %}
  <a target="_blank" href="{{ post.url }}">
  	<div style="border-bottom: 1px solid #c0c0c0; margin-bottom: 50px;">
  		<h2>{{ post.title }}</h2>
  		<img src="{{ post.image }}" style="max-height: 150px;">
  		<p>{{ post.date | date_to_string }}</p>
  	</div>
  </a>
{% endfor %}
</div>