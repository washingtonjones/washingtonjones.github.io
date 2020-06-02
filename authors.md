---
title: Authors
---
# Authors

{% for author in site.authors %}
- ## [{{ author.name }}]({{ author.url | relative_url }})
  ### {{ author.position }}
  {{ author.content | markdownify }}
{% endfor %}