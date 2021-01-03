---
permalink: /
title: "Andy Clifton"
excerpt: "About me"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

Originally trained as a mechanical engineer, I work to enable the global deployment of renewable energy. I do this through my own research; by sharing what I do with others; and by helping others to share their work. 

Checkout [my portfolio](/projects), [writing](/blog), or [biography](/bio) for more information.


## Recent writing
{% include base_path %}
{% assign posts = site.posts | where_exp:"post","post.draft != true" | sort: "date" | reverse %}
<div class="container">
<div class="row mb-1">
{% for post in posts limit:3 %}
<div class="col-12 col-md-6 col-lg-4 col-xl-4 mb-1 mx-0 px-1">
{% include archive-single-card.html %}
</div>
{% endfor %}
</div>
</div>
[Read more of my writing](/blog).

## My portfolio
{% include base_path %}
{% assign projects = site.projects | where_exp:"project","project.draft != true" | sort: "date" | reverse %}
<div class="container">
<div class="row mb-3">
{% for post in projects limit:5 %}
<div class="col-12 col-md-6 col-lg-4 col-xl-4 mb-1 mx-0 px-1">
{% include archive-single-card.html %}
</div>
{% endfor %}
</div>
</div>
[See more of my projects](/projects).