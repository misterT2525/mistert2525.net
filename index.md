---
layout: page
title: misterT
tagline: (ミスターT, misterT2525)
---
{% include JB/setup %}

TODO: 後で書く

## Recent Posts

<div class="row">
  {% for post in site.posts limit:3 %}
  <div class="col-sm-6 col-md-4">
    <div class="thumbnail">
      {% if post.thumbnail %}<img src="{{ post.thumbnail }}" alt="{{ post.title }}">{% endif %}
      <div class="caption">
        <h3>{{ post.title }}</h3>
        <p>{{ post.description }}</p>
        <p><a href="{{ BASE_PATH }}{{ post.url }}" class="btn btn-default" role="button">READ MORE</a></p>
      </div>
    </div>
  </div>
  {% endfor %}
</div>
