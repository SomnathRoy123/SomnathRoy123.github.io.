---
layout: page
permalink: /publications/
title: Publications
description: My published work and ongoing research manuscripts.
nav: true
nav_order: 2
---

{% include bib_search.liquid %}

<div class="publications">

## Manuscripts in Preparation
{% bibliography -q @unpublished %}

## Published Papers
{% bibliography -q @article %}

</div>