---
layout: default
title: "서비스"
description: "공명이 만들고 운영하는 서비스 목록입니다."
permalink: /services/
---

# 서비스

공명이 만들고 운영하는 서비스입니다.

<div class="card-grid">
  {% assign sorted_services = site.services | sort: "order" %}
  {% for service in sorted_services %}
  <div class="card">
    <h3><a href="{{ service.url | relative_url }}">{{ service.title }}</a></h3>
    <p>{{ service.summary }}</p>
  </div>
  {% endfor %}
</div>
