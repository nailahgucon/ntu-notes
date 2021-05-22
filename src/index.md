---
title: Hello World
layout: "base.njk"
---

Helloooooo world

{% for note in collections.notes %}

- [{{ note.data.title }}]({{ note.url }})

{% endfor %}