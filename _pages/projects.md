---
layout: default
title: <Your Name> - Portfolio
permalink: /projects/
---

<div class="gallery-container">
<div class="project-gallery">
    {% for project in site.projects %}
      {% if project.title != "Open Design Project Pitch" and project.title != "Functional Prototype" %}
      <div class="gallery-item">
        <a href="{{ project.url | relative_url }}">
          <img src="{{ project.image | default: "/assets/images/default-project.jpg" | relative_url }}" alt="{{ project.title }}" class="project-image" />
          <p>{{ project.title}}</p>
        </a>
      </div>
      {% endif %}
    {% endfor %}
</div>
</div>