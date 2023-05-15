---
title: "Don't be a fool, 차곡차곡 알아가는 IT지식!"
layout: archive
permalink: categories/it
author_profile: true
sidebar_main: true
---

<!-- 공백이 포함되어 있는 카테고리 이름의 경우 site.categories['a b c'] 이런식으로! -->

***

{% assign posts = site.categories.IT %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}