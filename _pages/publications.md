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

{% comment %}
Group publications by type and sort by year
{% endcomment %}

{% assign grouped_publications = site.publications | group_by: 'type' %}
{% assign sorted_groups = grouped_publications | sort: 'name' %}

{% for group in sorted_groups %}
  {% assign sorted_posts = group.items | sort: 'date' | reverse %}
  
  {% if sorted_posts.size > 0 %}
    <section class="publication-group">
      <h2 class="archive__subtitle">{{ group.name | default: "Other Publications" }}</h2>
      
      {% for post in sorted_posts %}
        {% include archive-single.html %}
      {% endfor %}
    </section>
  {% endif %}
  
{% endfor %}