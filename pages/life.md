---
layout: page
title: Life
description: 分享感悟
keywords: Tangled thoughts
comments: false
menu: Life
permalink: /life/
---

<ul class="listing">
    {% for tep in site.life %}
        {% if tep.tags contains 'life' and tep.title !="Life template"%}
                <li><span class="posts-list-meta">{{ tep.date | date:"%Y-%m-%d" }}</span>
                      <a class="posts-list-name" href="{{ site.url }}{{ tep.url }}">{{ tep.title }}</a>
                </li>
        {% endif %}
    {% endfor %}
</ul>

<!-- /section.content -->

