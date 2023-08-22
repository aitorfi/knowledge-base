---
layout: default
title: Home
nav_order: 1
---

# Knowledge base

My personal knowledge base, a wiki containing notes on IT stuff.
{: .fs-6 .fw-300 }

[GitHub repo](https://github.com/aitorfi/knowledge-base){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }

## Table of contents

<div>
    {% for collection in site.collections %}
        {% if collection.label != "posts" %}
            <h3>{{ collection.name }}</h3>
            <ul>
                {% for item in site[collection.label] %}
                    {% if item.parent == nil %}
                        <li><a href="{{site.baseurl}}{{ item.url }}">{{ item.title }}</a></li>
                    {% endif %}
                {% endfor %}
            </ul>
        {% endif %}
    {% endfor %}
</div>
