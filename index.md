<div class="ix">
<p class="ix-lead">X에서 AI · Robotics · Insights 주제로 모은 글과, 바로 써먹을 팁을 쌓아 두는 곳.</p>
<a class="ix-tips" href="{{ '/tips.html' | relative_url }}">팁 모음 보기</a>
</div>

<h2 class="ix-h">다이제스트</h2>
<ul class="ix-list">
{% assign ds = site.pages | where_exp: "p", "p.dir == '/digests/'" | sort: "name" | reverse %}{% for p in ds %}<li><a href="{{ p.url | relative_url }}">{{ p.name | remove: '.md' }}</a></li>
{% endfor %}</ul>
