---
layout: page
permalink: /publications/
title: Publications
description: A collection of my published research, peer-reviewed articles, and ongoing manuscripts.
nav: true
nav_order: 2
---

{% include bib_search.liquid %}

<div class="publications">

  <h3 class="mt-4 mb-2" style="border-bottom: 1px solid #e0e0e0; padding-bottom: 5px;">Manuscripts in Preparation</h3>
  <p class="text-muted mb-4"><small><em>Research currently undergoing data synthesis, drafting, or peer review.</em></small></p>
  {% bibliography -q @unpublished %}

  <h3 class="mt-5 mb-2" style="border-bottom: 1px solid #e0e0e0; padding-bottom: 5px;">Published Papers</h3>
  <p class="text-muted mb-4"><small><em>Peer-reviewed articles and conference proceedings.</em></small></p>
  {% bibliography -q @article %}

</div>