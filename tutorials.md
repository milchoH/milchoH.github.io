---
title: Tutorials
layout: default
permalink: tutorials

---
# Tutorials

## Tutorials place

<div id="archives">
{% for category in site.categories %}
  <div class="archive-group">
    {% capture category_name %}{{ category | first }}{% endcapture %}
    <div id="#{{ category_name | slugize }}"></div>
    <p></p>  
    <a name="{{ category_name | slugize }}"></a>
    {% for post in site.categories[category_name] %}
    <article class="archive-item">
      <h3><a href="{{ site.baseurl }}{{ post.url }}">{{post.title}}</a></h3>
    </article>
    {% endfor %}
  </div>
{% endfor %}
</div>
[Back to Home](./)