---
layout: default
---

  {% assign post = site.posts.first %}
  {% assign content = post.content %}
  {% assign author = site.authors[post.author] %}
  {% include post_detail.html %}
  {% include archive.md %}