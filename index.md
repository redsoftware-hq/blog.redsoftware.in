---
layout: default
---
{% if site.posts.size > 0 %}
<ul>
    {% for post in site.posts %}
    <li>
        <span>{{ post.date | date: "%b %-d, %Y" }}</span>
        <span><a href="{{post.url}}">{{post.title}}</a></span>
    </li>
    {% endfor %}
</ul>
{% else %}
<p style="color: #999; text-align: center;">No Posts Yet</p>
{% endif %}
