---
layout: page
permalink: /teaching/
title: Teaching
description: Teaching and mentoring experience
nav: true
nav_order: 6
---

<div class="projects">
<h3>Debug Check:</h3>
<p>Number of courses found: {{ site.teaching.size }}</p>
  {% for course in site.teaching %}
    <div class="row mb-4">
      <div class="col-sm-10">
        <h3 class="font-weight-bold">
          <a href="{{ course.url | relative_url }}">{{ course.title }}</a>
        </h3>
        <h5 class="font-italic">
          {{ course.role }} | {{ course.year }}
        </h5>
        <p>{{ course.description }}</p>
      </div>
    </div>
  {% endfor %}
</div>