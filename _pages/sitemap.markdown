---
layout: archive
title: "Sitemap"
permalink: /sitemap/
author_profile: false
---

Una lista con todos los posts del sitio.
<h2>Paginas</h2>
{% for post in site.pages %}
  {% include archive-single.html %}
{% endfor %}

<h2>Posts</h2>
{% for post in site.posts %}
  {% include archive-single.html %}
{% endfor %}
