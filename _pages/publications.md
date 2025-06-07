---
layout: archive
title: "Research & Publication"
permalink: /publications/
author_profile: true
---

{% if author.googlescholar %}
  You can also find my articles on <u><a href="{{author.googlescholar}}">my Google Scholar profile</a>.</u>
{% endif %}

{% include base_path %}

{% comment %} Define custom sort order {% endcomment %}
{% assign type_order = "Work in Progress,Academic Article,Report,Policy Brief,Op-Ed,Publication in Bahasa Indonesia" | split: "," %}

{% comment %} Group publications by type {% endcomment %}
{% assign grouped_pubs = site.publications | group_by: 'type' %}

{% comment %} Display publications in custom order {% endcomment %}
{% for type_name in type_order %}
  {% assign current_group = grouped_pubs | where: "name", type_name | first %}
  {% if current_group.items.size > 0 %}
    
## {{ type_name }}

{% assign sorted_items = current_group.items | sort: 'date' | reverse %}
{% for post in sorted_items %}
{% include archive-single.html %}
{% endfor %}
  {% endif %}
{% endfor %}

{% comment %} Display any remaining types not in the predefined order {% endcomment %}
{% for group in grouped_pubs %}
  {% unless type_order contains group.name %}
    {% if group.items.size > 0 %}
      
## {{ group.name | default: "Other" }}

{% assign sorted_items = group.items | sort: 'date' | reverse %}
{% for post in sorted_items %}
{% include archive-single.html %}
{% endfor %}
    {% endif %}
  {% endunless %}
{% endfor %}