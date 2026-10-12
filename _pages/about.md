---
layout: page
permalink: /about/
title: About
nav: true
nav_order: 1
---

I am a native of Lafayette, Colorado.
Outside the lab, I enjoy rock climbing, hiking, skiing, camping, ultimate frisbee, and exploring the outdoors.

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
