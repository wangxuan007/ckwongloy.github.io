---
layout: blog_backbone
title: Tag @ckwongloy
---

<a name="top"></a>

<section class="main-content" style="font-family:Georgia;">
<div class="home">
<h3 class="page-heading">
<strong>
<a href="/home/" title="Bak to Home">
<i class="fa fa-home"> Home</i></a>
<i class="fa fa-angle-double-right" style="color:silver;"></i>
<i class="fa fa-tags"> Tag</i>
<i class="fa fa-terminal" style="color:red;"></i></strong></h3>

<h2 style="text-align:center;">
<i class="fa fa-bolt"></i>
<i class="fa fa-bolt"></i>
<i class="fa fa-bolt"></i>
Now and Up-growing
&times;

{{ site.tags | size }}

</h2>

<div style="margin-bottom:90%;margin-top:10%;">

{% assign first = site.tags.first %}
{% assign max = first[1].size %}
{% assign min = max %}
{% for tag in site.tags offset:1 %}
{% if tag[1].size > max %}
{% assign max = tag[1].size %}
{% elsif tag[1].size < min %}
{% assign min = tag[1].size %}
{% endif %}
{% endfor %}
{% assign diff = max | minus: min %}

{% for tag in site.tags %}
{% assign temp = tag[1].size | minus: min | times: 35 | divided_by: diff %}
{% assign base = temp | divided_by: 3 %}
{% assign remain = temp | modulo: 4 %}
{% if remain == 0 %}
{% assign size = base | plus: 10 %}
{% elsif remain == 1 or remain == 2 %}
{% assign size = base | plus: 9 | append: '.5' %}
{% else %}
{% assign size = base | plus: 10 %}
{% endif %}
{% if remain == 0 or remain == 1 %}
{% assign color = 9 | minus: base %}
{% else %}
{% assign color = 8 | minus: base %}
{% endif %}

<span style="padding:3px; margin:3px; float:left; background:white; background:#BFD9DB; border-radius:100%;">
<a href="#{{ tag[0] }}" style="font-size: {{ size }}pt;color: #{{ color }}{{ color }}{{ color }};">

{{ tag[0] }}

</a>
<span style="color: #{{ color }}{{ color }}{{ color }};">

<sup>
{{ tag | last | size }}
</sup>

</span></span>

{% endfor %}

</div>
<h2 style="text-align:center;">
<i class="fa fa-bolt"></i>
<i class="fa fa-bolt"></i>
<i class="fa fa-bolt"></i>
<strong>
Details
</strong></h2>

{% for tag in site.tags %}

<p style="font-size:24px;margin-left:5%;">
<i class="fa fa-tag"></i>
<a href="#{{ tag | first }}" name="{{ tag | first }}" title="All posts below are taged by &lt;{{ tag | first }}&gt;">

{{ tag | first }}

</a>

<sup>
{{ tag | last | size }}
</sup>

</p>
<ul>

{% for post in tag.last %}

<ol>
<i class="fa fa-calendar"></i>

{{ post.date | date:"%Y-%m-%d"}}

<i class="fa fa-terminal"></i>
<a href="{{ post.url }}">

{{ post.title }}

</a></ol>

{% endfor %}

</ul>

{% endfor %}

</div></section>
