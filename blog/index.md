---
layout: default
title: All Blog Posts
---
# H1 {{ page.title }}

{% for post in site.posts %}

        * {{ post.date | date_to_string }} » [{{ post.title }}]({{ post.url }})
            {{ post.excerpt | remove: '<p>' | remove: '</p>' }}
    <
{% endfor %}