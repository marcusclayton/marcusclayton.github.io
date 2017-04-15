---
layout: default
---

  {% assign post = site.posts.first %}
  {% assign content = post.content %}
  {% include post_detail.html %}
  {% include archive.md %}
  {% include gitfooter.html %}
