---
permalink: /
title: "Dr. Yi Gao's Homepage"
layout: archive
author_profile: true
redirect_from: 
  - /about/
  - /about.html
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


<br>
*Professor* (教授)<br>
*Ph.D. Advisor* (博导)<br>
Department of Software Engineering (软件工程系)，系主任<br>
College of Computer Science and Technology (计算机科学与技术学院)<br>
Zhejiang University (浙江大学)<br>
Mail: 310027, Zetong Building, Yuquan Campus, Zhejiang University, Hangzhou, China<br>
Email: gaoyi AT zju.edu.cn<br>


Biography
========
Yi GAO (高艺) is currently a professor at the [College of Computer Science and Technology](http://www.cs.zju.edu.cn/), [Zhejiang University](https://www.zju.edu.cn/), China. He is a member of the [EmNets research group](https://www.emnets.cn) and the [EagleLab](http://eagle.zju.edu.cn/) at Zhejiang University. He previously served as a postdoctoral researcher at [McGill University](https://www.mcgill.ca/), Canada. He received his B.S. and Ph.D. degrees in Zhejiang University in 2009 and 2014, respectively. His research interests include IoT, wireless and mobile computing, and edge AI.

Teaching
========
CS3258M Fundamentals and Application Development for Internet of Things (物联网技术基础与应用开发), 2024Fall<br>
CS3136M Computer Networks (计算机网络), 2024Fall, 2023Fall, 2022Fall, 2021Fall, 2020Fall, 2019Fall<br>
Fundamentals and Applications of the Internet of Things (物联网基础与应用), 2018Fall<br>
Advanced Internet of Things Applications (高级物联网应用), 2017Fall<br>


Selected Publications <span style="font-size: 0.9em; font-weight: normal;">([full list](/publications/))</span>
========
<h3><em>Textbook</em></h3>
董玮, <u>高艺</u>, 韩劲松. "从创意到原型：物联网应用快速开发(第二版)", 科学出版社, 2022, ISBN 978-7-03-072966-8. (工信部“十四五”规划教材，浙江省普通高校“十三五”新形态教材，物联网工程专业系列教材)<br>

{% assign selected_venue_keywords = "NSDI,INFOCOM,IPSN,MOBICOM,TMC,ATC,TC,TOSN,ToN,TPDS,ICDCS,ICNP,MOBISYS,SENSYS,UBICOMP,WWW,PERCOM,SIGMETRICS,RTSS" | split: "," %}
<!-- 显示 Conference Papers -->
<h3><em>Conference Papers</em></h3>
<ul>
{% assign conference_papers = site.publications | where: 'publication_type', 'conference' | sort: 'date' | reverse %}
{% for paper in conference_papers %}
  {% assign venue_downcased = paper.venue | remove: '(' | remove: ')' | remove: ' ' | downcase %} 
  {%- if venue_downcased contains 'poster' or venue_downcased contains 'demo' or venue_downcased contains 'workshop' -%}
    {%- continue -%}
  {%- endif -%} 
  {% for keyword in selected_venue_keywords %}
    {% assign keyword_downcased = keyword | downcase %}
    {% if venue_downcased contains keyword_downcased %}
      <li>
        [<span style="color:red;">{{keyword}}</span>]
        {% for author in paper.authors %}
          {% if author == "Yi Gao" and paper.corresponding_authors contains author %}
            <u>{{ author }}</u>*{% unless forloop.last %}, {% endunless %}{%if forloop.last %}.{% endif %}
          {% elsif author == "Yi Gao"%}
            <u>{{ author }}</u>{% unless forloop.last %}, {% endunless %}{%if forloop.last %}.{% endif %}
          {% elsif  paper.corresponding_authors contains author%}
            {{ author }}*{% unless forloop.last %}, {% endunless %}{%if forloop.last %}.{% endif %}
          {% else %}
            {{ author }}{% unless forloop.last %}, {% endunless %}{%if forloop.last %}.{% endif %}
          {% endif %}          
        {% endfor %}
        <em>"{{ paper.title }}"</em>,
        <strong>{{ paper.venue }}</strong>,
        {% if paper.location %}
          {{ paper.location }}, 
        {% endif %}
        {{ paper.date | default: "1901-01-01" | date: "%Y" }}.
        {% if paper.paperurl %}
          <a href=" {{ paper.paperurl }} ">Download Paper</a>
        {% endif %}  
      </li>
      {% break %}
    {% endif %}
  {% endfor %}
{% endfor %}
</ul>

<!-- 显示 Journal Articles -->
<h3><em>Journal Articles</em></h3>
<ul>
{% assign journal_articles = site.publications | where: 'publication_type', 'journal' | sort: 'date' | reverse %}
{% for article in journal_articles %}
  {% assign venue_downcased = article.venue | remove: '(' | remove: ')' | remove: ' ' | downcase %}
  {% for keyword in selected_venue_keywords %}
    {% assign keyword_downcased = keyword | downcase %}
    {% if venue_downcased contains keyword_downcased %}
      <li>
        [<span style="color:red;">{{keyword}}</span>]
        {% for author in article.authors %}
          {% if author == "Yi Gao" and article.corresponding_authors contains author %}
            <u>{{ author }}</u>*{% unless forloop.last %}, {% endunless %}{%if forloop.last %}.{% endif %}
          {% elsif author == "Yi Gao"%}
            <u>{{ author }}</u>{% unless forloop.last %}, {% endunless %}{%if forloop.last %}.{% endif %}
          {% elsif  article.corresponding_authors contains author%}
            {{ author }}*{% unless forloop.last %}, {% endunless %}{%if forloop.last %}.{% endif %}
          {% else %}
            {{ author }}{% unless forloop.last %}, {% endunless %}{%if forloop.last %}.{% endif %}
          {% endif %}          
        {% endfor %}
        <em>"{{ article.title }}"</em>,
        <strong>{{ article.venue }}</strong>,
        {% if article.vol_no_pp and article.vol_no_pp != "nan" %}
          {{ article.vol_no_pp }},
        {% endif %} 
        {% if article.location %}
          {{ article.location }}, 
        {% endif %}
        {{ article.date | default: "1901-01-01" | date: "%Y" }}.
        {% if article.paperurl %}
          <a href=" {{ article.paperurl }} ">Download Paper</a>
        {% endif %}   
      </li>
      {% break %}
    {% endif %}
  {% endfor %}
{% endfor %}
</ul>

