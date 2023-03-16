<<<<<<< HEAD
# All my public Repositorys
=======
>>>>>>> 54ef276 (Repositorys)
{% for repository in site.github.public_repositories %}
  * [{{ repository.name }}]({{ repository.html_url }})
{% endfor %}
# All my private Repositorys
{% for repository in site.github.private_repositories %}
  * [{{ repository.name }}]({{ repository.html_url }})
{% endfor %}