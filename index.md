---
layout: default
---
{% assign author = site.authors[page.author] %}
  {% assign post = site.posts.first %}
  Author: [{{ author.display_name }}](https://github.com/{{ author.github }})
  {% assign content = post.content %}
  {% include post_detail.html %}
  {% include archive.md %}