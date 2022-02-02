---
title: "Recursion"
layout: archive
permalink: categories/recursion
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.recursion %}

{% for post in posts %} {% include archive-single2.html type=page.entries_layout %}{% endfor %}
