---
layout: default
permalink: /blog/
title: blog
nav: true
nav_order: 1
pagination:
  enabled: true
  collection: posts
  permalink: /page/:num/
  per_page: 5
  sort_field: date
  sort_reverse: true
  trail:
    before: 1 
    after: 3 
---

<style>
  /* Academic Elegance Styles */
  .academic-header {
    margin-bottom: 3rem;
    border-bottom: 1px solid #eaeaea;
    padding-bottom: 1.5rem;
  }
  .academic-header h1 {
    font-weight: 700;
    color: #2c3e50;
    letter-spacing: -0.5px;
  }
  
  /* Featured Posts */
  .featured-wrapper {
    background: #fdfdfd;
    border-left: 4px solid #3498db;
    padding: 2rem;
    box-shadow: 0 4px 15px rgba(0,0,0,0.03);
    border-radius: 0 8px 8px 0;
    margin-bottom: 3rem;
    transition: transform 0.2s ease, box-shadow 0.2s ease;
  }
  .featured-wrapper:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(0,0,0,0.06);
  }
  .featured-label {
    font-family: 'Courier New', monospace;
    font-size: 0.85rem;
    color: #e74c3c;
    text-transform: uppercase;
    letter-spacing: 1px;
    margin-bottom: 1rem;
    display: block;
  }

  /* List Items */
  .post-item {
    padding: 2rem 0;
    border-bottom: 1px solid #f0f0f0;
    transition: background 0.3s ease;
  }
  .post-item:hover {
    background: #fafafa;
    border-radius: 8px;
    padding: 2rem 1.5rem;
    margin-left: -1.5rem;
    margin-right: -1.5rem;
  }
  
  /* Typography */
  .post-title {
    font-size: 1.6rem;
    font-weight: 600;
    color: #2c3e50;
    text-decoration: none;
    line-height: 1.3;
    transition: color 0.2s;
  }
  .post-title:hover {
    color: #3498db;
    text-decoration: none;
  }
  .post-meta {
    font-family: 'Courier New', monospace;
    font-size: 0.85rem;
    color: #7f8c8d;
    margin: 0.8rem 0 1.2rem 0;
  }
  .post-abstract {
    color: #444;
    line-height: 1.7;
    font-size: 1.05rem;
  }
  
  /* Modern Minimalist Tags */
  .tag-badge {
    display: inline-block;
    border: 1px solid #bdc3c7;
    color: #7f8c8d;
    padding: 0.2rem 0.8rem;
    border-radius: 20px;
    font-size: 0.75rem;
    text-transform: lowercase;
    text-decoration: none;
    transition: all 0.2s ease;
    margin-right: 0.5rem;
  }
  .tag-badge:hover {
    border-color: #3498db;
    color: #3498db;
    background: rgba(52, 152, 219, 0.05);
    text-decoration: none;
  }
</style>

<div class="post">

  {% assign blog_name_size = site.blog_name | size %}
  {% assign blog_description_size = site.blog_description | size %}

  {% if blog_name_size > 0 or blog_description_size > 0 %}
  <div class="academic-header">
    <h1>{{ site.blog_name }}</h1>
    <h2 style="font-size: 1.2rem; color: #7f8c8d; font-weight: 300;">{{ site.blog_description }}</h2>
  </div>
  {% endif %}

  {% assign featured_posts = site.posts | where: "featured", "true" %}
  {% if featured_posts.size > 0 %}
  <div class="row row-cols-1 g-4 mb-5">
    {% for post in featured_posts %}
    <div class="col">
      <a href="{{ post.url | relative_url }}" style="text-decoration: none; color: inherit;">
        <div class="featured-wrapper">
          <span class="featured-label"><i class="fa-solid fa-star fa-xs"></i> Highlighted Research</span>
          
          <h3 class="post-title">{{ post.title }}</h3>
          
          {% if post.external_source == blank %}
            {% assign read_time = post.content | number_of_words | divided_by: 180 | plus: 1 %}
          {% else %}
            {% assign read_time = post.feed_content | strip_html | number_of_words | divided_by: 180 | plus: 1 %}
          {% endif %}
          
          <div class="post-meta">
            {{ post.date | date: "%B %d, %Y" }} &middot; {{ read_time }} min read
          </div>
          
          <p class="post-abstract"><strong>Abstract:</strong> {{ post.description }}</p>
        </div>
      </a>
    </div>
    {% endfor %}
  </div>
  {% endif %}

  <div class="post-list-container">
    {% if page.pagination.enabled %}
      {% assign postlist = paginator.posts %}
    {% else %}
      {% assign postlist = site.posts %}
    {% endif %}

    {% for post in postlist %}

    {% if post.external_source == blank %}
      {% assign read_time = post.content | number_of_words | divided_by: 180 | plus: 1 %}
    {% else %}
      {% assign read_time = post.feed_content | strip_html | number_of_words | divided_by: 180 | plus: 1 %}
    {% endif %}

    <div class="post-item">
      {% if post.thumbnail %}
      <div class="row align-items-center">
        <div class="col-md-9">
      {% endif %}
      
      <h3>
        {% if post.redirect == blank %}
          <a class="post-title" href="{{ post.url | relative_url }}">{{ post.title }}</a>
        {% elsif post.redirect contains '://' %}
          <a class="post-title" href="{{ post.redirect }}" target="_blank">{{ post.title }} <i class="fa-solid fa-arrow-up-right-from-square fa-xs" style="color: #bdc3c7;"></i></a>
        {% else %}
          <a class="post-title" href="{{ post.redirect | relative_url }}">{{ post.title }}</a>
        {% endif %}
      </h3>

      <div class="post-meta">
        {{ post.date | date: '%Y-%m-%d' }} &nbsp;&middot;&nbsp; {{ read_time }} min read
        {% if post.external_source %}
        &nbsp;&middot;&nbsp; {{ post.external_source }}
        {% endif %}
      </div>

      <p class="post-abstract">{{ post.description }}</p>

      <div class="mt-3">
        {% for category in post.categories %}
          <a href="{{ category | slugify | prepend: '/blog/category/' | relative_url }}" class="tag-badge">{{ category }}</a>
        {% endfor %}
        {% for tag in post.tags %}
          <a href="{{ tag | slugify | prepend: '/blog/tag/' | relative_url }}" class="tag-badge">#{{ tag }}</a>
        {% endfor %}
      </div>

      {% if post.thumbnail %}
        </div>
        <div class="col-md-3 mt-3 mt-md-0">
          <img class="img-fluid rounded" src="{{ post.thumbnail | relative_url }}" style="object-fit: cover; width: 100%; box-shadow: 0 4px 8px rgba(0,0,0,0.1);" alt="Thumbnail for {{ post.title }}">
        </div>
      </div>
      {% endif %}
    </div>

    {% endfor %}
  </div>

  {% if page.pagination.enabled %}
  <div class="mt-5">
    {% include pagination.liquid %}
  </div>
  {% endif %}

</div>