# My public Repositorys
{% for repository in site.github.public_repositories %}
  * [{{ repository.name }}]({{ repository.html_url }})
{% endfor %}
# Ausführlicher
{% for repository in site.github.public_repositories %}
  <h3>{{ repository.name }}</h3>
  <p>{{ repository.description }}</p>
  <p>Sprache: {{ repository.language }}</p>
  <p>Sterne: {{ repository.stargazers_count }}</p>
{% endfor %}