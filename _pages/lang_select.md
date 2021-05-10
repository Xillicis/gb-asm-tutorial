---
permalink: /start
---

# Select a language

{% for lang in site.data.pages %}
- [{{ lang[1].name }}]({{ site.baseurl }}/{{ lang[0] }}/part1/setup)
{% endfor %}
