---
layout: page
permalink: /publications/
title: publications
description: Work that I have authored or co-authored. See [Inspire HEP](https://inspirehep.net/authors/2661508) for all my work.
sections:
  - bibquery: "@article"
    text: "Journal articles"
  - bibquery: "@inproceedings"
    text: "Conference proceedings"
  # - bibquery: "@phdthesis"
  #   text: "PhD thesis"
  - bibquery: "@mastersthesis"
    text: "Masters thesis"
social: true
nav: true
nav_order: 2
---

{% include bib_search.liquid %}

<div class="publications">

{%- for section in page.sections %}
  <h2 id="{{section.text}}">{{section.text}}</h2>

    {%- comment -%}  Count bibliography in actual section and year {%- endcomment -%}
    {%- capture citecount -%}
    {%- bibliography_count -f {{site.scholar.bibliography}} -q {{section.bibquery}} -%}
    {%- endcapture -%}

    {%- comment -%} If exist bibliography in actual section and year, print {%- endcomment -%}
    {%- if citecount !="0" %}

      {% bibliography -f {{site.scholar.bibliography}} -q {{section.bibquery}} %}

    {%- endif -%}

{%- endfor %}

</div>
