---
title: Dev 
permalink: /dev
layout: page
---

{%- assign sortedTags = site.tags | sort -%}

<div class="tag-list">

{% for tag in sortedTags %}

	<a href="#{{tag[0]}}">{{ tag[0] }}&nbsp;({{ tag[1] | size }})</a>

{% endfor %}

</div>

{% for tag in sortedTags %}

<section class="posts-by-tag">

<h2 id="{{ tag[0] }}">{{ tag[0] }}</h2>

{% for post in tag[1] %}
{% include blog-listing.html %}
{% endfor %}

<a href="#" class="internal-link">All Tags &#8593;</a>

{% endfor %}


