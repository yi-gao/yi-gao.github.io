---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---

<style>
ul {
  list-style-type: none; /* 移除项目符号 */
  padding: 0; /* 移除列表的内边距 */
  margin: 0; /* 移除列表的外边距 */
}

li {
  line-height: 1.3; /* 减小行间距，数值越小，间距越小 */  
  margin-bottom: 3px; /* 减少底部外边距，数值越小，间距越小 */
}
</style>


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
{% assign before_2015 = false %}
<ul>
{% for post in published_posts%}
  {% assign this_year = post.date | date: "%Y" %}
  {% if current_year != this_year and before_2015 != true %}
    {% if current_year != nil %}
      </ul>
    {% endif %}
    {% if this_year == "2015" %}
      {% assign before_2015 = true %}
    {% endif %}
    {% if before_2015 %}
      <h2>2015 and Before</h2>
    {% else %}
      <h2>{{ this_year }}</h2>
    {% endif %}
    <ul>
    {% assign current_year = this_year %}
  {% endif %}
  {% assign counter = counter | plus: 1 %}
  <li>
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
  {% if post.vol_no_pp and post.vol_no_pp != "nan" %}
    {{ post.vol_no_pp }},
  {% endif %} 
  {% if post.location %}
    {{ post.location }}, 
  {% endif %}
  {{ post.date | default: "1901-01-01" | date: "%Y" }}.
  {% if post.paperurl %}
    <a href=" {{ post.paperurl }} ">Download Paper</a>
  {% endif %}
  </li>
{% endfor %}
</ul>
{% if current_year != nil %}
</ul>
{% endif %}
