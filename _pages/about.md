---
layout: page
permalink: /about/
title: About
nav: true
nav_order: 1
---

I was born and raised in Lafayette, Colorado, where I attended Centaurus High School and graduated in 2021 (sko warriors!). I took a gap year away from academia to take a break from online school, working on small scale residential remodels with <a href="https://www.carvecolorado.com/" target="_blank" rel="noopener noreferrer">Carve Construction</a> in Boulder, Colorado. Then I spent four years in Schenectady, New York, studying mechanical engineering and mathematics at Union College (sko chargers!), where I picked up ultimate frisbee. Recently, I moved out to the bay area to pursue a Ph.D. in mechanical engineering at the University of California, Berkeley. 

Outside the lab, I enjoy cycling, hiking, skiing, ultimate frisbee, and exploring the outdoors. My favorite weekend activity is to grab my road bike, plan a fun route, and go exploring on new roads in my area (especially if they are very hilly).

<style>
  .interest-galleries { display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 2rem; margin-top: 2.5rem; }
  .interest-section { min-width: 0; }
  .interest-gallery figure { margin: 0; }
  .interest-gallery a { display: block; border-radius: 10px; overflow: hidden; }
  .interest-gallery a:focus-visible, .interest-controls button:focus-visible { outline: 3px solid currentColor; outline-offset: 4px; }
  .interest-gallery img { display: block; width: 100%; aspect-ratio: 4 / 3; object-fit: contain; background: rgba(127, 127, 127, 0.1); }
  .interest-gallery [hidden] { display: none !important; }
  .interest-controls { display: flex; flex-wrap: wrap; align-items: center; justify-content: center; gap: 0.5rem; margin-top: 0.75rem; }
  .interest-controls button { color: inherit; background: transparent; border: 1px solid currentColor; border-radius: 6px; padding: 0.35rem 0.65rem; cursor: pointer; }
  .interest-counter { font-size: 0.9rem; min-width: 4rem; text-align: center; }
  @media (max-width: 600px) { .interest-galleries { grid-template-columns: 1fr; } }
</style>

<!-- Add photos and captions in _data/about_interests.yml. -->
<div class="interest-galleries">
{% for interest in site.data.about_interests %}
<section class="interest-section" aria-labelledby="{{ interest.id }}">
  <h2 id="{{ interest.id }}">{{ interest.title }}</h2>
  <p>{{ interest.description }}</p>
  <div class="interest-gallery" data-gallery role="region" aria-roledescription="carousel" aria-label="{{ interest.title }} photos">
    {% for photo in interest.photos %}
    <figure data-slide role="group" aria-roledescription="slide" aria-label="{{ forloop.index }} of {{ interest.photos.size }}"{% unless forloop.first %} hidden{% endunless %}>
      <a href="{{ photo.src | relative_url | uri_escape }}" target="_blank" rel="noopener noreferrer" aria-label="Open photo: {{ photo.alt | escape }}">
        <img {% if forloop.first %}src{% else %}data-src{% endif %}="{{ photo.src | relative_url | uri_escape }}" alt="{{ photo.alt | escape }}" loading="lazy" decoding="async" width="800" height="600">
      </a>
      {% if photo.caption and photo.caption != '' %}
      <figcaption>{{ photo.caption | escape }}</figcaption>
      {% endif %}
    </figure>
    {% endfor %}
    <div class="interest-controls" data-controls hidden>
      <button type="button" data-previous aria-label="Previous {{ interest.title }} photo">Previous</button>
      <span class="interest-counter" data-counter aria-live="off">1 / {{ interest.photos.size }}</span>
      <button type="button" data-next aria-label="Next {{ interest.title }} photo">Next</button>
      <button type="button" data-pause aria-label="Pause {{ interest.title }} slideshow">Pause</button>
    </div>
  </div>
</section>
{% endfor %}
</div>

<script>
(() => {
  const reducedMotion = window.matchMedia("(prefers-reduced-motion: reduce)");
  document.querySelectorAll("[data-gallery]").forEach((gallery) => {
    const slides = Array.from(gallery.querySelectorAll("[data-slide]"));
    if (slides.length < 2) return;
    const counter = gallery.querySelector("[data-counter]");
    const pause = gallery.querySelector("[data-pause]");
    const title = gallery.getAttribute("aria-label");
    let index = 0;
    let playing = !reducedMotion.matches;
    let timer;
    const show = (next) => {
      slides[index].hidden = true;
      index = (next + slides.length) % slides.length;
      const image = slides[index].querySelector("img");
      if (image.dataset.src) {
        image.src = image.dataset.src;
        delete image.dataset.src;
      }
      slides[index].hidden = false;
      counter.textContent = (index + 1) + " / " + slides.length;
    };
    const sync = () => {
      window.clearInterval(timer);
      pause.textContent = playing ? "Pause" : "Play";
      pause.setAttribute("aria-label", (playing ? "Pause " : "Play ") + title);
      if (playing && !document.hidden && !gallery.matches(":hover") && !gallery.contains(document.activeElement)) {
        timer = window.setInterval(() => show(index + 1), 5000);
      }
    };
    gallery.querySelector("[data-controls]").hidden = false;
    gallery.querySelector("[data-previous]").addEventListener("click", () => { show(index - 1); sync(); });
    gallery.querySelector("[data-next]").addEventListener("click", () => { show(index + 1); sync(); });
    pause.addEventListener("click", () => { playing = !playing; sync(); });
    gallery.addEventListener("mouseenter", sync);
    gallery.addEventListener("mouseleave", sync);
    gallery.addEventListener("focusin", sync);
    gallery.addEventListener("focusout", () => window.setTimeout(sync, 0));
    document.addEventListener("visibilitychange", sync);
    reducedMotion.addEventListener("change", () => { playing = !reducedMotion.matches; sync(); });
    sync();
  });
})();
</script>
