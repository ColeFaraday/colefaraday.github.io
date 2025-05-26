---
layout: default
permalink: /posts/
title: posts
nav: false
nav_order: 4
pagination:
  enabled: true
  collection: posts
  permalink: /page/:num/
  per_page: 5
  sort_field: date
  sort_reverse: true
  trail:
    before: 1 # The number of links before the current page
    after: 3 # The number of links after the current page
---

<div class="post">

{% assign notes_name_size = site.notes_name | size %}
{% assign notes_description_size = site.notes_description | size %}

{% if notes_name_size > 0 or notes_description_size > 0 %}
  <div class="header-bar">
    <h1>{{ site.notes_name }}</h1>
    <h2>{{ site.notes_description }}</h2>
  </div>
{% endif %}

{% if site.display_tags and site.display_tags.size > 0 or site.display_categories and site.display_categories.size > 0 %}
  <div class="tag-category-list">
    <ul class="p-0 m-0">
      {% for tag in site.display_tags %}
        <li>
          <i class="fa-solid fa-hashtag fa-sm"></i> <a href="{{ tag | slugify | prepend: '/notes/tag/' | relative_url }}">{{ tag }}</a>
        </li>
        {% unless forloop.last %}<p>&bull;</p>{% endunless %}
      {% endfor %}
      {% if site.display_categories.size > 0 and site.display_tags.size > 0 %}
        <p>&bull;</p>
      {% endif %}
      {% for category in site.display_categories %}
        <li>
          <i class="fa-solid fa-tag fa-sm"></i> <a href="{{ category | slugify | prepend: '/notes/category/' | relative_url }}">{{ category }}</a>
        </li>
        {% unless forloop.last %}<p>&bull;</p>{% endunless %}
      {% endfor %}
    </ul>
  </div>
{% endif %}

{% assign featured_notes = site.notes | where: "featured", "true" %}
{% if featured_notes.size > 0 %}
<br>
<div class="container featured-posts">
  {% assign is_even = featured_notes.size | modulo: 2 %}
  <div class="row row-cols-{% if featured_notes.size <= 2 or is_even == 0 %}2{% else %}3{% endif %}">
    {% for note in featured_notes %}
    <div class="col mb-4">
      <a href="{{ note.url | relative_url }}">
        <div class="card hoverable">
          <div class="row g-0">
            <div class="col-md-12">
              <div class="card-body">
                <div class="float-right">
                  <i class="fa-solid fa-thumbtack fa-xs"></i>
                </div>
                <h3 class="card-title text-lowercase">{{ note.title }}</h3>
                <p class="card-text">{{ note.description }}</p>

                {% assign read_time = note.content | number_of_words | divided_by: 180 | plus: 1 %}
                {% assign year = note.date | date: "%Y" %}

                <p class="post-meta">
                  {{ read_time }} min read &nbsp; &middot; &nbsp;
                  <a href="{{ year | prepend: '/notes/' | relative_url }}">
                    <i class="fa-solid fa-calendar fa-sm"></i> {{ year }}
                  </a>
                </p>
              </div>
            </div>
          </div>
        </div>
      </a>
    </div>
    {% endfor %}
  </div>
</div>
<hr>
{% endif %}

<ul class="post-list">

  {% assign notelist = site.notes %}

  {% for note in notelist %}
    {% assign read_time = note.content | number_of_words | divided_by: 180 | plus: 1 %}
    {% assign year = note.date | date: "%Y" %}
    {% assign tags = note.tags | join: "" %}
    {% assign categories = note.categories | join: "" %}

    <li>
      {% if note.thumbnail %}
      <div class="row">
        <div class="col-sm-9">
      {% endif %}

      <h3>
        <a class="post-title" href="{{ note.url | relative_url }}">{{ note.title }}</a>
      </h3>
      <p>{{ note.description }}</p>
      <p class="post-meta">
        {{ read_time }} min read &nbsp; &middot; &nbsp;
        {{ note.date | date: '%B %d, %Y' }}
      </p>
      <p class="post-tags">
        <a href="{{ year | prepend: '/notes/' | relative_url }}">
          <i class="fa-solid fa-calendar fa-sm"></i> {{ year }}
        </a>

        {% if tags != "" %}
        &nbsp; &middot; &nbsp;
        {% for tag in note.tags %}
          <a href="{{ tag | slugify | prepend: '/notes/tag/' | relative_url }}">
            <i class="fa-solid fa-hashtag fa-sm"></i> {{ tag }}</a>{% unless forloop.last %}&nbsp;{% endunless %}
        {% endfor %}
        {% endif %}

        {% if categories != "" %}
        &nbsp; &middot; &nbsp;
        {% for category in note.categories %}
          <a href="{{ category | slugify | prepend: '/notes/category/' | relative_url }}">
            <i class="fa-solid fa-tag fa-sm"></i> {{ category }}</a>{% unless forloop.last %}&nbsp;{% endunless %}
        {% endfor %}
        {% endif %}
      </p>

      {% if note.thumbnail %}
        </div>
        <div class="col-sm-3">
          <img class="card-img" src="{{ note.thumbnail | relative_url }}" style="object-fit: cover; height: 90%" alt="image">
        </div>
      </div>
      {% endif %}
    </li>
  {% endfor %}
</ul>

</div>
