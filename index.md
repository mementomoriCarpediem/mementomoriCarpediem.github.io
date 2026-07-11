---
layout: default
description: "공명은 일상의 문제를 기술로 풀어내는 서비스들을 만듭니다. 선(한)결제, ContextVoca, Katchi를 만들고 있습니다."
---

# 공명

<p class="lead">공명은 일상의 문제를 기술로 풀어내는 서비스들을 만듭니다. 작은 불편함을 찾아 담백하게 해결하는 것을 지향합니다.</p>

## 우리가 하는 일

공명은 여러 개의 독립적인 서비스를 만들고 운영합니다. 각 서비스는 서로 다른 문제를 다루지만, "사용자의 일상에 실질적인 도움이 되는가"라는 같은 질문에서 출발합니다.

## 서비스 소개

<div class="card-grid">
  {% assign sorted_services = site.services | sort: "order" %}
  {% for service in sorted_services %}
  <div class="card">
    <h3><a href="{{ service.url | relative_url }}">{{ service.title }}</a></h3>
    <p>{{ service.summary }}</p>
  </div>
  {% endfor %}
</div>

<p><a href="{{ '/services/' | relative_url }}">전체 서비스 보기 →</a></p>

## 문의

서비스 관련 문의는 이메일로 연락해 주세요: <a href="mailto:resonance.zorba@gmail.com">resonance.zorba@gmail.com</a>
