---
layout: page
title: projects
permalink: /projects/
description: A growing collection of research and computational projects.
nav: true
nav_order: 3
display_categories: [Biophysics, Machine Learning, Computational Data Science, Open Source]
horizontal: false
masonry: false
---

<style>
  /* 1. The Sticky Navigation Bar (Clean & Text-Based) */
  .academic-nav-wrapper {
    position: sticky;
    top: 60px; /* Adjusts based on your main navbar height */
    z-index: 1000;
    background: rgba(255, 255, 255, 0.95); /* Slight transparency */
    backdrop-filter: blur(5px);
    border-bottom: 1px solid #eaeaea;
    padding: 15px 0;
    margin-bottom: 3rem;
  }

  .academic-nav {
    display: flex;
    justify-content: center;
    gap: 30px;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
  }

  .academic-nav a {
    color: #555;
    text-decoration: none;
    font-size: 0.85rem;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 1px; /* Wide spacing looks more premium */
    transition: color 0.2s ease;
  }

  .academic-nav a:hover {
    color: #000;
    text-decoration: underline;
    text-decoration-thickness: 2px;
  }

  /* 2. Professional Section Headers */
  .academic-header {
    margin-top: 4rem;
    margin-bottom: 2rem;
    border-bottom: 1px solid #333; /* Solid black line */
    padding-bottom: 10px;
    display: flex;
    align-items: baseline;
  }

  .academic-number {
    font-family: "Georgia", "Times New Roman", serif;
    font-size: 1.5rem;
    color: #999;
    margin-right: 15px;
    font-style: italic;
  }

  .academic-title {
    font-family: "Georgia", "Times New Roman", serif; /* Academic Standard */
    font-size: 2rem;
    font-weight: 700;
    color: #111;
    margin: 0;
  }

  .project-count-sub {
    font-size: 0.85rem;
    color: #777;
    margin-left: auto; /* Pushes count to the far right */
    font-family: sans-serif;
  }
</style>

{% if site.enable_project_categories and page.display_categories %}

<div class="academic-nav-wrapper">
  <div class="academic-nav">
    {% for category in page.display_categories %}
      <a href="#{{ category | slugify }}">{{ category }}</a>
    {% endfor %}
  </div>
</div>

<div class="projects">
  
  {% for category in page.display_categories %}
  {% assign categorized_projects = site.projects | where: "category", category %}
  {% assign sorted_projects = categorized_projects | sort: "importance" %}
  
  <div id="{{ category | slugify }}" class="category-section">
    
    <div class="academic-header">
      <span class="academic-number">0{{ forloop.index }}.</span>
      <h2 class="academic-title">{{ category }}</h2>
      <span class="project-count-sub">{{ categorized_projects.size }} Projects</span>
    </div>

    <div class="row row-cols-1 row-cols-md-3">
      {% for project in sorted_projects %}
        {% include projects.liquid %}
      {% endfor %}
    </div>
  </div>
  {% endfor %}

</div>

{% else %}

{% assign sorted_projects = site.projects | sort: "importance" %}
<div class="row row-cols-1 row-cols-md-3">
  {% for project in sorted_projects %}
    {% include projects.liquid %}
  {% endfor %}
</div>

{% endif %}