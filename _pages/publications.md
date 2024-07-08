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

{% assign to_appear_posts = site.publications | where_exp: "post", "post.to_appear == true" %}
{% assign counter = 0 %}


<ul>
<h2>To Appear</h2>
<ul>
{% for post in to_appear_posts %}
  {% assign counter = counter | plus: 1 %}
    [{{ counter }}]    
    {% for author in post.authors %}
      {% if author == "Yi Gao" %}
        <u>{{ author }}</u>{% unless forloop.last %}, {% endunless %}
      {% else %}
        {{ author }}{% unless forloop.last %}, {% endunless %}
      {% endif %}
    {% endfor %}. 
    <em>"{{ post.title }}"</em>,
    <em>{{ post.venue }} (To Appear)</em>.    
{% endfor %}
</ul>
</ul>


{% assign published_posts = site.publications | where_exp: "post", "post.to_appear != true" | sort: 'date' | reverse %}
{% assign current_year = nil %}
<ul>
{% for post in published_posts%}
  {% assign this_year = post.date | date: "%Y" %}
  {% if current_year != this_year %}
    {% unless current_year == nil %}
      </ul>
    {% endunless %}
    <h2>{{ this_year }}</h2>
    <ul>
    {% assign current_year = this_year %}
  {% endif %}
  {% assign counter = counter | plus: 1 %}
    [{{ counter }}]    
    {% for author in post.authors %}
      {% if author == "Yi Gao" %}
        <u>{{ author }}</u>{% unless forloop.last %}, {% endunless %}
      {% else %}
        {{ author }}{% unless forloop.last %}, {% endunless %}
      {% endif %}
    {% endfor %}.
    <em>"{{ post.title }}"</em>.
    <em>{{ post.venue }}</em>,
    {% if post.vol_no_pp %}
      {{ post.vol_no_pp }}, 
    {% endif %}
    {% if post.location %}
      {{ post.location }}, 
    {% endif %}
    {{ post.date | default: "1901-01-01" | date: "%Y" }}.
    {% if post.paperurl %}
      <a href=" {{ post.paperurl }} ">Download Paper</a>
    {% endif %}
    <br>
{% endfor %}
</ul>
{% if current_year != nil %}
</ul>
{% endif %}
