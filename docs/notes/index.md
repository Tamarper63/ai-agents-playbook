---
title: Notes
permalink: /notes/
---

# Notes

Long-form technical writeups.

## Topics

- [Agent architecture]({{ '/notes/agent-architecture/' | relative_url }})
- [Agent security]({{ '/notes/agent-security/' | relative_url }})
- [Model training and evaluation]({{ '/notes/model-training-and-eval/' | relative_url }})

## Latest notes (all topics)

<ul>
{% assign note_pages = site.pages | sort: "url" %}
{% for p in note_pages %}
  {% if p.url contains '/notes/' and p.url != page.url and p.title %}
    {% unless p.url contains '/notes/agent-architecture/' or p.url contains '/notes/agent-security/' or p.url contains '/notes/model-training-and-eval/' %}
      <!-- If you keep topic index pages as standalone pages, they will still appear unless they lack title -->
    {% endunless %}
    {% unless p.url endswith '/notes/' %}
      {% unless p.url endswith '/notes/agent-architecture/' %}
        {% unless p.url endswith '/notes/agent-security/' %}
          {% unless p.url endswith '/notes/model-training-and-eval/' %}
            <li>
              <a href="{{ p.url | relative_url }}">{{ p.title }}</a>
              {% if p.summary %} — {{ p.summary }}{% endif %}
            </li>
          {% endunless %}
        {% endunless %}
      {% endunless %}
    {% endunless %}
  {% endif %}
{% endfor %}
</ul>
