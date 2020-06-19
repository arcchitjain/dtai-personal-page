---
layout: page
permalink: /teaching/
title: Teaching
description: List of courses I helped teaching
---

{% for item in site.teaching %}
  <div>
    <em>{{ item.period }}</em>:
    <strong>
        {{ item.course }}
    </strong>

  	{% if item.note %}
	    <p>
	    	{{ item.note }}
	    </p>
  	{% endif %}
  </div>
{% endfor %}