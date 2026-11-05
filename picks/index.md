---
title: 골라 온 글
---
<div class="ix">
<h1>골라 온 글</h1>
<p class="ix-lead" style="margin-top:14px; color:var(--ink)">직접 가져온 X 글을 한국어로 정리해 둔 곳. 원문 링크를 함께 둔다.</p>
</div>

<h2 class="ix-h">글 목록</h2>
{% assign ps = site.pages | where_exp: "p", "p.dir == '/picks/'" | where_exp: "p", "p.name != 'index.md'" | sort: "name" | reverse %}
{% if ps.size == 0 %}<p class="es-d">아직 글이 없습니다.</p>{% endif %}
<ul class="ix-list es-list">
{% for p in ps %}<li><a href="{{ p.url | relative_url }}"><span class="es-t">{{ p.title }}</span><span class="es-d">{{ p.date | date: "%Y-%m-%d" }}</span></a></li>
{% endfor %}</ul>
