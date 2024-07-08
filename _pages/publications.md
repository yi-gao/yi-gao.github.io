---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---

{% if site.author.googlescholar %}
  <div class="wordwrap">You can also find my articles on <a href="{{site.author.googlescholar}}">my Google Scholar profile</a>.</div>
{% endif %}

{% include base_path %}

{% for post in site.publications reversed %}
{% assign counter = counter | plus: 1 %}
  <p>         
    [{{ counter }}],   
    {{ post.authors | join: ', ' }}, 
    "{{ post.title }}",
    {{ post.venue }},
    {{ post.location }}, {{ post.date | default: "1900-01-01" | date: "%Y" }},
    {% if post.paperurl%}
      <p><a href=" {{ post.paperurl }} ">Download Paper</a></p>
  </p>
{% endfor %}
