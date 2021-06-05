---
title: Intro to Computational Thinking and Programming
---

## weomce to ICT
<br>
<div class="card-div">
{%- for post in collections.ICTP-code -%}
    <div class="card">
    <h3>{{ post.data.pageTitle }}</h3>
    <p class="card-p"><a href="{{ post.url }}" class="card-a">Go to page to view &raquo;</a></p>
    </div>
{%- endfor -%}
</div>