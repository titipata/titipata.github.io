---
title: Blog
permalink: /blog/
---

<div class="content list">

  {% for post in site.posts %}
    <div class="list-item">
      <p class="list-post-title">
        <a href="{{ site.baseurl }}{{ post.url }}">- {{ post.title }}</a>
      </p>
    </div>
  {% endfor %}

</div>
