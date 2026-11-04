# mrtmi x digest

X에서 AI · Robotics · Insights 주제로 모은 글과 팁을 쌓아 두는 곳.

- **[팁 모음](tips.html)**

## 다이제스트
{% assign ds = site.pages | where_exp: "p", "p.dir == '/digests/'" | sort: "name" | reverse %}
{% for p in ds %}- [{{ p.name | remove: '.md' }}]({{ p.url | relative_url }})
{% endfor %}
