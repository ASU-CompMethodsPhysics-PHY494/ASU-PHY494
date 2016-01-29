---
layout: page
title: Overview
---

{% comment %}
Generate a list for all "posts", i.e. the content pages, in
chronological order.
{% endcomment %}

The lessons in chronological order so far:

<ol class="nonumbers">
{% assign pages_list = site.posts | sort:"url" %}
	{% for node in pages_list %}
	   {% if node.title != null %}
            {% if node.layout == "post" %}
				<li><a href="{{ site.baseurl }}{{ node.url }}">{{ node.title }}</a></li>
			{% endif %}
	   {% endif %}
    {% endfor %}
</ol>

