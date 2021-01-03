---
permalink: /
title: "Andy Clifton"
excerpt: "About me"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

Harvesting renewable energy from the wind, sun, biomass, rivers and seas will give more people reliable access to safe energy. Over the last three decades wind and solar energy have gone from being a tiny part of the energy supply to supplying up to a half of the annual energy needs of many countries, and are now cheaper than most alternative sources of energy.

But deploying renewable energy is a big challenge that cannot be achieved without lots of different groups working together. We need to identify and test new technologies, get them into the hands of the organisations and companies that can commercialise them, and then install them worldwide. We need to keep them running, and then get energy to the people that need it. At the same time we need to protect people and the environment from potential negative impacts, too. And we need to keep doing this, every day.

Because the change to renewable energy is quite literally a challenge for a generation, international collaboration between academia and industry is essential. Academics and researchers are our source of ideas and train new workers, while those folks that actually get out there and install the turbines or solar panels pull those ideas through the technology transfer pipeline. 

I work to enable the global deployment of renewable energy by priming that pipeline and helping industry access the ideas coming out of research. I also help researchers understand what is needed by industry. I do this through my work with several R&D networks, by encouraging open science, and by directly engaging in my own areas of expertise.

When I'm not working you'll find me on a bicycle somewhere, or up a mountain.

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