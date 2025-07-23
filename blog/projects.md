---
layout: default
title: Projects
permalink: /blog/projects/
---
# 🚀 Projects

Welcome to the Projects page! Here you'll find a collection of articles and resources related to various DevOps projects.

{% for post in site.categories.projects %}
- [{{ post.title }}]({{ post.url }})
{% endfor %}