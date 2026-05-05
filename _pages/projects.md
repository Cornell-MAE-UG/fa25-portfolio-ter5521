---
layout: default
title: <Your Name> - Portfolio
permalink: /projects/
---

<div class="gallery-container">
<div class="project-gallery">
    {% assign hidden_projects = "Open Design Project Pitch,Functional Prototype,Client Pitch,Client Report" | split: "," %}
    {% for project in site.projects %}
      {% unless hidden_projects contains project.title %}
      <div class="gallery-item">
        <a href="{{ project.url | relative_url }}">
          <img src="{{ project.image | default: "/assets/images/default-project.jpg" | relative_url }}" alt="{{ project.title }}" class="project-image" />
          <p>{{ project.title}}</p>
        </a>
      </div>
      {% endunless %}
    {% endfor %}
</div>
</div>