---
layout: page
title: Site map
root: .
---

{% assign sorted_pages = (site.pages | sort: 'title') %}
{% for p in sorted_pages %}
  {% if p.title and p.title != page.title %}
  {% assign purl = site.baseurl | append:p.url %}
  <nav>
    <a href="{{ purl }}">{{ p.title }}</a>
    {% assign h2chunks = p.content | split:'<h2 id="' %}
    {% if h2chunks.size > 1 %}
      <ul>
      {% for h2chunk in h2chunks offset:1 %}
        {% assign h2 = h2chunk | split:'</h2>' %}
        {% assign id_text = h2[0] | split:'">' %}
        <li>
         <a href="{{ purl }}#{{ id_text[0] }}">{{ id_text[1] }}</a>
        </li>
        {% assign h3chunks = h2[1] | split:'<h3 id="' %}
        {% if h3chunks.size > 1 %}
        <ul>
        {% for h3chunk in h3chunks offset:1 %}
          {% assign h3 = h3chunk | split:'</h3>' %}
          {% assign id_text = h3[0] | split:'">' %}
          <li>
           <a href="{{ purl }}#{{ id_text[0] }}">{{ id_text[1] }}</a>
          </li>
        {% endfor %}
        </ul>
        {% endif %}
      {% endfor %}
      </ul>
    {% endif %}
  </nav>
  {% endif %}
{% endfor %}
