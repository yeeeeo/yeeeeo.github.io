---
title: "The heroes are born in xell / 비전공자 데이터 청년 캠퍼스 후기."
layout: archive
permalink: categories/data-campus
author_profile: true
sidebar_main: true
---

<!-- 공백이 포함되어 있는 카테고리 이름의 경우 site.categories['a b c'] 이런식으로! -->

***

{% assign posts = site.categories.Data-campus %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}