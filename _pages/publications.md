---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---

{% if author.googlescholar %}
  You can also find my articles on <u><a href="{{author.googlescholar}}">my Google Scholar profile</a>.</u>
{% endif %}

{% include base_path %}

{% assign grouped_pubs = site.publications | group_by: 'type' %}

{% for group in grouped_pubs %}
  {% if group.items.size > 0 %}
    <h2>{{ group.name | default: "Other" }}</h2>
    {% assign sorted_items = group.items | sort: 'date' | reverse %}
    {% for post in sorted_items %}
      {% include archive-single.html %}
    {% endfor %}
  {% endif %}
{% endfor %}