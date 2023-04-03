---
lang: de
title: Dokumentation
permalink: /
---
Willkommen zur Dokumentation der Veranstaltungsdatenbank.

<strong>Du bist neu hier?</strong> Dann empfehlen wir die Anleitung [Erste Schritte]({% post_url /guide/2023-04-01-first-steps %}).

## Kategorien

<ul>
{% for category in site.categories %}
    {% assign first_category = category | first %}
    <li><a href="{{ site.url }}/category/{{ category | first | slugify }}/index.html">{{ site.data.lang.categories[first_category] }}</a>
</li>
{% endfor %}
</ul>

## Neueste Einträge

{% for post in site.posts limit:5 %}
<div class="card mt-4">
  <div class="card-body">
    <h5 class="card-title">{{ post.title }}</h5>
    <h6 class="card-subtitle mb-2 text-muted">{{ post.date | date: site.data.lang.date_format }} &sdot; {% for category in post.categories %}{{ site.data.lang.categories[category] }}{% endfor %}</h6>
    <p class="card-text">{{ post.excerpt }}</p>
    <a href="{{ post.url }}" class="card-link stretched-link">{{ site.data.lang.excerpt_more }}</a>
  </div>
</div>
{% endfor %}