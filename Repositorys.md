# My public Repositorys
{% for repository in site.github.public_repositories %}
  * [{{ repository.name }}]({{ repository.html_url }})
{% endfor %}
# Ausführlicher
{% for repository in site.github.public_repositories %}
## [{{ repository.name }}]({{ repository.html_url }})
  * {{ repository.description }}
  * Sprache: {{ repository.language }}
  * Sterne: {{ repository.stargazers_count }}
{{ repository.homepage_url }}  

{% endfor %}