---
layout: page
title: Post by Category
permalink: /categoryview/
sitemap: false
---
    
<div>
 <ul class="categorie-tags">
    {% assign categories = site.categories | sort %}
    {% for category in categories %}
    
    <li class="categorie-tag">
     
        <a href="#{{ category | first | slugify }}">
                {{ category[0] | replace:'-', ' ' }} ({{ category | last | size }})
        </a>
    
    </li>
    {% endfor %}
 </ul>
</div>
    
<div id="index">

        {% for category in categories %}
        <a name="{{ category[0] }}"></a><h2>{{ category[0] | replace:'-', ' ' }} ({{ category | last | size }}) </h2>
        {% assign sorted_posts = site.posts | sort: 'title' %}
        {% for post in sorted_posts %}
        {%if post.categories contains category[0]%}

        <h4 class="post-title">
                <a href="{{ site.url }}{{site.baseurl}}{{ post.url }}" title="{{ post.title }}">{{ post.title }} 
                        <p class="date">{{ post.date |  date: "%B %e, %Y" }}</p>
                </a>
        </h4>
        <p>{{ post.excerpt | strip_html | truncate: 160 }}</p>

        {%endif%}
        {% endfor %}

        {% endfor %}
</div>
