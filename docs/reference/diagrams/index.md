---
title: Diagrams
permalink: /reference/diagrams/
summary: Index of technical diagrams with captions and text alternatives.
---

This index lists technical diagrams.

**Conventions (page-level contract):**
- Each diagram page should include a **caption** and short **alt text**.
- Complex diagrams should additionally include a **text alternative (long description)** to meet the intent of WCAG text-alternatives guidance.

{% assign cats = site.data.diagrams.categories %}

{% if cats %}
<nav id="categories" class="page-toc page-toc--inline" aria-label="Diagram categories">
  <div class="page-toc__title">Categories</div>
  <ul class="page-toc__list">
    {% for cat in cats %}
      <li><a href="#{{ cat.id }}">{{ cat.title }}</a></li>
    {% endfor %}
  </ul>
</nav>

{% for cat in cats %}
<section aria-labelledby="{{ cat.id }}">
  <h2 id="{{ cat.id }}">{{ cat.title }}</h2>

  <ul>
    {% for d in cat.items %}
      {% assign p = site.pages | where: "url", d.url | first %}
      <li>
        <strong><a href="{{ d.url | relative_url }}">{{ d.title }}</a></strong><br/>
        {{ d.summary }}

        {% if p %}
          {% assign has_links = "" %}
          {% if p.diagram_asset %}{% assign has_links = "1" %}{% endif %}
          {% if p.diagram_source_path %}{% assign has_links = "1" %}{% endif %}

          {% if has_links == "1" %}
            <div>
              Links:
              <a href="{{ d.url | relative_url }}">Page</a>
              {% if p.diagram_asset %}
                · <a href="{{ p.diagram_asset | relative_url }}">Image</a>
                {% assign fmt = p.diagram_asset | split: '.' | last | upcase %}
                <span>({{ fmt }})</span>
              {% endif %}
              {% if p.diagram_source_path %}
                · <a href="{{ p.diagram_source_path | relative_url }}">Source</a>
              {% endif %}
            </div>
          {% endif %}
        {% endif %}
      </li>
    {% endfor %}
  </ul>

  <p><a href="#categories">Back to categories</a></p>
</section>
{% endfor %}

{% else %}
NOT VERIFIED: site.data.diagrams.categories is missing, so this index cannot render categories.
{% endif %}