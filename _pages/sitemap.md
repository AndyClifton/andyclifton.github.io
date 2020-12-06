---
layout: archive
title: "Sitemap"
permalink: /sitemap/
author_profile: true
---

{% include base_path %}

A list of all the posts and pages found on the site. For you robots out there is an [XML version]({{ base_path }}/sitemap.xml) available for digesting as well.

<h2>Pages</h2>
<ul>
{% assign pl = site.pages | sort:"title" %}
{% for post in pl %}
{% if post.title =='' or post.title==nil%}
{% else %}
  {% include archive-pages-single-li.html %}
{% endif %}
{% endfor %}
</ul>

<h2>My writing</h2>
<div class="container">
  <div class="row mb-1">
{% for post in site.posts %}
  <div class="col-12 col-md-6 col-lg-4 col-xl-4 mb-1 mx-0 px-1">
      {% include archive-single-card.html %}
    </div>    
{% endfor %}
</div>
</div>

<h2>My projects</h2>
<div class="container">
  <div class="row mb-1">
{% for post in site.projects %}
  <div class="col-12 col-md-6 col-lg-4 col-xl-4 mb-1 mx-0 px-1">
      {% include archive-single-card.html %}
    </div>    
{% endfor %}
</div>
</div>

