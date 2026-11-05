<div class="ix">
<p class="ix-lead">X에서 AI · Robotics · Insights 주제로 모은 글과, 바로 써먹을 팁을 쌓아 두는 곳.</p>
<div class="btns"><a class="btn" href="{{ '/tips.html' | relative_url }}">팁 모음 보기</a><a class="btn btn-line" href="{{ '/picks/' | relative_url }}">골라 온 글</a><a class="btn btn-line" href="{{ '/essays/' | relative_url }}">에세이</a></div>
</div>

<h2 class="ix-h">다이제스트</h2>
{% assign ds = site.pages | where_exp: "p", "p.dir == '/digests/'" | sort: "name" | reverse %}<div class="cals" id="cals" data-base="{{ '/digests/' | relative_url }}" data-days="{% for p in ds %}{{ p.name | remove: '.md' }} {% endfor %}"></div>
<noscript><ul class="ix-list">{% for p in ds %}<li><a href="{{ p.url | relative_url }}">{{ p.name | remove: '.md' }}</a></li>{% endfor %}</ul></noscript>

<script>
// 다이제스트가 있는 날만 링크인 달력. 첫 다이제스트가 나온 달부터 이번 달까지, ‹ › 로 넘긴다.
(function () {
  var box = document.getElementById('cals'), base = box.dataset.base;
  var days = new Set(box.dataset.days.trim().split(/\s+/).filter(Boolean));
  var z = function (n) { return String(n).padStart(2, '0'); };
  var t = new Date(), today = t.getFullYear() + '-' + z(t.getMonth() + 1) + '-' + z(t.getDate());
  var first = Array.from(days).sort()[0] || today, y = +first.slice(0, 4), m = +first.slice(5, 7), months = [];
  while (y < t.getFullYear() || (y === t.getFullYear() && m <= t.getMonth() + 1)) { months.push([y, m]); if (m === 12) { y++; m = 1; } else m++; }
  var i = months.length - 1;
  function render() {
    var y = months[i][0], m = months[i][1], cells = [], n = new Date(y, m, 0).getDate();
    for (var k = new Date(y, m - 1, 1).getDay(); k > 0; k--) cells.push('');
    for (var d = 1; d <= n; d++) {
      var key = y + '-' + z(m) + '-' + z(d);
      cells.push(days.has(key) ? '<a href="' + base + key + '.html" aria-label="' + m + '월 ' + d + '일 다이제스트">' + d + '</a>'
        : key === today ? '<b aria-current="date">' + d + '</b>' : '<span>' + d + '</span>');
    }
    while (cells.length % 7) cells.push('');
    var rows = '';
    for (var r = 0; r < cells.length; r += 7) rows += '<tr>' + cells.slice(r, r + 7).map(function (c) { return '<td>' + c + '</td>'; }).join('') + '</tr>';
    box.innerHTML = '<div class="cal-nav"><button type="button" data-d="-1" aria-label="이전 달"' + (i === 0 ? ' disabled' : '') + '>‹</button>'
      + '<button type="button" data-d="1" aria-label="다음 달"' + (i === months.length - 1 ? ' disabled' : '') + '>›</button></div>'
      + '<table class="cal"><caption>' + y + '년 ' + m + '월</caption><thead><tr>'
      + '일월화수목금토'.split('').map(function (w) { return '<th>' + w + '</th>'; }).join('') + '</tr></thead><tbody>' + rows + '</tbody></table>';
    box.querySelectorAll('.cal-nav button').forEach(function (b) {
      b.addEventListener('click', function () { i = Math.min(months.length - 1, Math.max(0, i + +b.dataset.d)); render(); box.querySelector('.cal-nav button:not([disabled])').focus(); });
    });
  }
  render();
})();
</script>
