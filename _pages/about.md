---
layout: page
permalink: /about/
title: About
nav: true
nav_order: 1
---

I was born and raised in Lafayette, Colorado, where I attended Centaurus High School and graduated in 2021 (sko warriors!). I took a gap year away from academia to take a break from online school, working on small scale residential remodels with <a href="https://www.carvecolorado.com/" target="_blank" rel="noopener noreferrer">Carve Construction</a> in Boulder, Colorado. Then I spent four years in Schenectady, New York, studying mechanical engineering and mathematics at Union College (sko chargers!), where I picked up ultimate frisbee and rock climbing. Recently, I moved out to the bay area to pursue a Ph.D. in mechanical engineering at the University of California, Berkeley. 

Outside the lab, I enjoy rock climbing, cycling, hiking, skiing, camping, ultimate frisbee, and exploring the outdoors. My favorite weekend activity is to grab my road bike, plan a fun route, and go exploring on new roads in my area (especially if they are very hilly).

<style>
  .interest-section { margin-top: 2.5rem; }
  .interest-gallery { display: grid; grid-template-columns: repeat(auto-fit, minmax(min(100%, 220px), 1fr)); gap: 1rem; margin-top: 1.25rem; }
  .interest-gallery figure { margin: 0; min-width: 0; }
  .interest-gallery a { display: block; border-radius: 10px; overflow: hidden; }
  .interest-gallery a:focus-visible { outline: 3px solid currentColor; outline-offset: 4px; }
  .interest-gallery img { display: block; width: 100%; aspect-ratio: 4 / 3; object-fit: cover; }
  .interest-photo-placeholder { display: flex; align-items: center; justify-content: center; aspect-ratio: 4 / 3; border: 1px dashed currentColor; border-radius: 10px; opacity: 0.55; font-size: 0.9rem; }
  .interest-gallery figcaption { margin-top: 0.5rem; font-size: 0.9rem; line-height: 1.5; }
</style>

<!-- Edit the section text, photo paths, and captions in _data/about_interests.yml. -->
{% for interest in site.data.about_interests %}
<section class="interest-section" aria-labelledby="{{ interest.id }}">
  <h2 id="{{ interest.id }}">{{ interest.title }}</h2>
  <p>{{ interest.description }}</p>
  <div class="interest-gallery" aria-label="{{ interest.title }} photos">
    {% for photo in interest.photos %}
    <figure>
      {% if photo.src and photo.src != '' %}
      <a href="{{ photo.src | relative_url }}" target="_blank" rel="noopener noreferrer" aria-label="Open photo: {{ photo.alt | escape }}">
        <img src="{{ photo.src | relative_url }}" alt="{{ photo.alt | escape }}" loading="lazy" width="800" height="600">
      </a>
      {% else %}
      <div class="interest-photo-placeholder">{{ interest.title }} photo {{ forloop.index }}</div>
      {% endif %}
      {% if photo.caption and photo.caption != '' %}
      <figcaption>{{ photo.caption | escape }}</figcaption>
      {% endif %}
    </figure>
    {% endfor %}
  </div>
</section>
{% endfor %}
