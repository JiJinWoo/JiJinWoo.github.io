---
title: "Math"
layout: archive
permalink: categories/math
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.math %}

{% for post in posts %} {% include archive-single2.html type=page.entries_layout %}{% endfor %}
