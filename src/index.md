---
title: Nailah's Notes Blog
layout: "base.njk"
---

Helloooooo world

{% for note in collections.notes %}

- [{{ note.data.title }}]({{ note.url }})

{% endfor %}