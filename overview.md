---
layout: page
title: Overview
---

{% comment %}
Generate a list for all "posts", i.e. the content pages, in
chronological order.
{% endcomment %}

The lessons in chronological order so far[^1] (the list will be complete
at the end of the semester):

<ol class="nonumbers">
{% assign pages_list = site.posts | sort:"url" %}
	{% for node in pages_list %}
	   {% if node.title != null %}
            {% if node.layout == "post" %}
				<li><a href="{{ site.baseurl }}{{ node.url }}">{{ node.title }}</a></li>
            {% assign lastdate = node.date %}
            {% endif %}
	   {% endif %}
    {% endfor %}
</ol>

Sometimes lessons span more than one lecture but this is not
explicitly marked. The dates associated with each lesson indicate the
day when the lesson was introduced for the first time.

Most of the teaching material is available as Jupyter notebooks and
linked from the lesson pages (typically, near the bottom). For
lessons in progress, links initially only point to incomplete
materials. Full materials including solutions to in-class problems are
always made available after the completion of the lesson.

----

[^1]:

     The most recent lesson in the list on this page started on
     {{ lastdate | date: "%B %-d, %Y" }}.
