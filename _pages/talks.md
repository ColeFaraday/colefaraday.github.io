---
layout: page
permalink: /talks/
title: talks
description: Talks and posters that I have presented.
nav: true
nav_order: 3
---

<!-- _pages/publications.md -->

<!-- Bibsearch Feature -->

{% include bib_search.liquid %}

<div class="publications">

{% bibliography -f {{ site.scholar.secondarybib }} %}

</div>
