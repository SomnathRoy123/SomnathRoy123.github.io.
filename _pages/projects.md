---
layout: page
title: projects
permalink: /projects/
description: A growing collection of research and computational projects.
nav: true
nav_order: 3
display_categories: [Biophysics, Machine Learning, Statistical Physics, Open Source]
horizontal: false
masonry: true
---

{% if site.enable_project_categories and page.display_categories %}
<div class="project-nav mb-4">
  <span class="mr-2 font-weight-bold">Jump to:</span>
  {% for category in page.display_categories %}
    <a href="#{{ category | slugify }}" class="badge badge-light text-uppercase p-2 mr-1" style="font-size: 0.85rem; border: 1px solid #ddd;">
      {{ category }}
    </a>
  {% endfor %}
</div>
{% endif %}

<div class="projects">
{% if site.enable_project_categories and page.display_categories %}
  
  {% for category in page.display_categories %}
  {% assign categorized_projects = site.projects | where: "category", category %}
  {% assign sorted_projects = categorized_projects | sort: "importance" %}

  <div id="{{ category | slugify }}" class="category-section mb-5">
    <div class="d-flex align-items-center mb-3">
      <h2 class="category mb-0 mr-3">{{ category }}</h2>
      <span class="text-muted" style="font-size: 0.9rem; font-style: italic;">
        {{ categorized_projects.size }} project{% if categorized_projects.size != 1 %}s{% endif %}
      </span>
    </div>
    <hr class="mt-0 mb-4" style="border-top: 1px solid #eaeaea;">

    {% if page.horizontal %}
    <div class="container">
      <div class="row row-cols-1 row-cols-md-2">
      {% for project in sorted_projects %}
        {% include projects_horizontal.liquid %}
      {% endfor %}
      </div>
    </div>
    {% else %}
    <div class="row row-cols-1 row-cols-md-3">
      {% for project in sorted_projects %}
        {% include projects.liquid %}
      {% endfor %}
    </div>
    {% endif %}
  </div>
  {% endfor %}

{% else %}

{% assign sorted_projects = site.projects | sort: "importance" %}
  {% if page.horizontal %}
  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}

{% endif %}
</div>