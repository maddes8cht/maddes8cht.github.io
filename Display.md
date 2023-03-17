---
title: Display
---
{% for image in site.static_files %}
{% if image.path contains 'images/slider' %}

![{{image.path}}]({{ site.baseurl }}{{ image.path }})
{% endif %}
{% endfor %}

