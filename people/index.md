---
layout: default
title: People
permalink: /people/
---

{% assign group_order = "Faculty,Students" | split: "," %}
{% assign grouped     = site.data.people | group_by: "group" %}

{% for group_name in group_order %}
## {{ group_name }}

<div class="people-grid">
  {% assign grp = grouped | where: "name", group_name | first %}
  {% if grp %}
    {% for p in grp.items %}
      <div class="person-card">
        <img src="{{ p.photo | relative_url }}" alt="{{ p.name }}">
        <h3>{{ p.name }}</h3>
        <p><em>{{ p.role }}</em></p>

        {% for r in p.research %}
          <p>
            <strong>{{ r.category }}:</strong>
            {{ r.topics | join: ", " }}
          </p>
        {% endfor %}

        <p><a href="mailto:{{ p.email }}">{{ p.email }}</a></p>
      </div>
    {% endfor %}
  {% endif %}
</div>

{% endfor %}

<style>
.people-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px,1fr));
  gap: 2rem;
}
.person-card {
  text-align: center;
}
.person-card img {
  width: 120px;
  height: auto;
  border-radius: .5rem;
  margin: 0 auto;
}
.person-card h3 {
  margin: .5rem 0 .25rem;
}
.person-card p {
  margin: .25rem 0;
  font-size: .9rem;
}
</style>
