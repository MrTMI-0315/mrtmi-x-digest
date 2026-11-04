---
title: 에세이
---
<div class="ix">
<h1>에세이</h1>
<p class="ix-lead" style="margin-top:14px; color:var(--ink)">다이제스트와 팁에서 걸린 것을 붙잡아 쓴 글.</p>
<div class="btns"><a class="btn" id="write" href="https://github.com/MrTMI-0315/mrtmi-x-digest/new/main/essays">새 글 쓰기</a></div>
</div>

<h2 class="ix-h">글 목록</h2>
{% assign es = site.pages | where_exp: "p", "p.dir == '/essays/'" | where_exp: "p", "p.name != 'index.md'" | sort: "name" | reverse %}
{% if es.size == 0 %}<p class="es-d">아직 글이 없습니다.</p>{% endif %}
<ul class="ix-list es-list">
{% for p in es %}<li><a href="{{ p.url | relative_url }}"><span class="es-t">{{ p.title }}</span><span class="es-d">{{ p.date | date: "%Y-%m-%d" }}</span></a></li>
{% endfor %}</ul>

<script>
// 오늘 날짜로 파일 이름과 글 틀을 채운 GitHub 새 파일 편집기를 연다
document.getElementById('write').addEventListener('click', function (e) {
  var d = new Date(), z = function (n) { return String(n).padStart(2, '0'); };
  var day = d.getFullYear() + '-' + z(d.getMonth() + 1) + '-' + z(d.getDate());
  var name = day + '-' + z(d.getHours()) + z(d.getMinutes()) + '.md';
  var body = '---\ntitle: 제목\ndate: ' + day + '\n---\n\n여기에 본문을 붙여 넣으세요. 다이제스트 링크는 [이렇게](https://mrtmi-0315.github.io/mrtmi-x-digest/) 걸면 됩니다.\n';
  this.href = 'https://github.com/MrTMI-0315/mrtmi-x-digest/new/main/essays?filename=' + encodeURIComponent(name) + '&value=' + encodeURIComponent(body);
});
</script>
