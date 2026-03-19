---
title: Updates
description: Release notes and update log for new policies, how-to guides, prompt assets, and articles on Andy Agent Lab.
permalink: /updates/
---

{% if site.data.updates.updates and site.data.updates.updates.size > 0 %}
Recent updates across policies, how-to guides, prompt assets, and articles.

<div class="c-grid c-grid--2">
  {% assign sorted = site.data.updates.updates | sort: 'date' | reverse %}
  {% for u in sorted %}
    <a class="c-card" href="{{ u.url | relative_url }}">
      <div class="c-card__content">
        <div class="c-card__title">{{ u.title }}</div>
        <div class="c-card__desc">{{ u.date }} · {{ u.type }}</div>
      </div>
    </a>
  {% endfor %}
</div>
{% else %}
No updates posted yet. You can follow via the [Newsletter]({{ '/newsletter/' | relative_url }}).
{% endif %}