---
title: Repos
layout: base
---
{:.no_toc}
# Repositories
{% for repository in site.github.public_repositories %}
  * [{{ repository.name }}]({{ repository.html_url }})
{% endfor %}
{:.no_toc}
# extended Repo Index
* Inhalt
{:toc}
{% for repository in site.github.public_repositories %}
## [{{ repository.name }}]({{ repository.html_url }})
  {{ repository.description }}
  * Sprache: {{ repository.language }}
  * Sterne: {{ repository.stargazers_count }}
{{ repository.homepage_url }}  

{% endfor %}