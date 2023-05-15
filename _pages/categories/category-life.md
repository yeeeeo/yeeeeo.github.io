---
title: "get away from my secret. 내 생활에 대한 이모조모 🍎🍏"
layout: archive
permalink: categories/life
author_profile: true
sidebar_main: true
---

<!-- 공백이 포함되어 있는 카테고리 이름의 경우 site.categories['a b c'] 이런식으로! -->

***

{% assign posts = site.categories.Life %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}