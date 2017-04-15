---
layout: default
---

  {% assign post = site.posts.first %}
  Author: {{ post.author }}
  {% assign content = post.content %}
  {% include post_detail.html %}
  {% include archive.md %}