---
layout: blog_backbone
title: Archive @ckwongloy
---

<a href="" name="top"></a>

<section class="main-content" style="font-family:Georgia;">
<div class="home">
<h3 class="page-heading">
<strong>
<a href="/home/" title="Bak to Home">
<i class="fa fa-home"> Home</i></a>
<i class="fa fa-angle-double-right" style="color:silver;"></i>
<i class="fa fa-archive"> Archive</i>
<i class="fa fa-terminal" style="color:red;"></i></strong></h3>

<h2 style="text-align:center;">
<i class="fa fa-bolt"></i>
<i class="fa fa-bolt"></i>
<i class="fa fa-bolt"></i>
Timeline &times;
{{ site.posts | size }}
</h2>

<div style="width:100%;">
<div style="width:40%;float:left;margin:30px;background:#F7F6F6;">
<h3>Month</h3>
{% assign count_by_month = 0 %}
{% for post in site.posts %}
{% capture this_month %}{{ post.date | date: "%Y 年 %m 月" }}{% endcapture %}
{% capture next_month %}{{ post.previous.date | date: "%Y 年 %m 月" }}{% endcapture %}
{% assign count_by_month = count_by_month| plus: 1 %}
{% if forloop.last or this_month != next_month %}
<li style="list-style:none;padding:2px;">
<i class="fa fa-archive"></i>
<a href="#{{ post.date | date: "%Y-%m" }}">
{{ post.date | date: "%Y 年 %m 月" }}
</a>
&lt;{{ count_by_month }}&gt;
</li>
{% assign count_by_month = 0 %}
{% endif %}
{% endfor %}
</div>
<div style="width:30%;float:left;margin:50px;background:#F7F6F6;">
<h3>Year</h3>
{% assign count_by_year = 0 %}
{% for post in site.posts %}
{% capture this_year %}{{ post.date | date: "%Y" }}{% endcapture %}
{% capture next_year %}{{ post.previous.date | date: "%Y" }}{% endcapture %}
{% assign count_by_year = count_by_year| plus: 1 %}
{% if forloop.last or this_year != next_year %}
<li style="list-style:none;padding:5px;">
<i class="fa fa-flag-checkered"></i>
<a href="#{{ post.date | date: "%Y" }}">
{{ this_year }}
</a>
&lt;{{ count_by_year }}&gt;
</li>
{% assign count_by_year = 0 %}
{% endif %}
{% endfor %}
</div></div>
<div style="margin-top:90%;">
<h2 style="text-align:center;">
<i class="fa fa-bolt"></i>
<i class="fa fa-bolt"></i>
<i class="fa fa-bolt"></i>
<strong>
Details
</strong></h2>
{% for post in site.posts  %}
{% capture this_year %}{{ post.date | date: "%Y" }}{% endcapture %}
{% capture this_month %}{{ post.date | date: "%B" }}{% endcapture %}
{% capture next_year %}{{ post.previous.date | date: "%Y" }}{% endcapture %}
{% capture next_month %}{{ post.previous.date | date: "%B" }}{% endcapture %}
{% if forloop.first %}
<h2 style="text-align:center; background:#BFD9DB;">
<i class="fa fa-flag-checkered"></i>
<a href="#{{ post.date | date: "%Y" }}" name="{{ post.date | date: "%Y" }}">
{{ this_year }}
</a></h2>
<h3>
<i class="fa fa-calendar-check-o"></i>
<a href="#{{ post.date | date: "%Y-%m" }}" name="{{ post.date | date: "%Y-%m" }}">
{{this_month}}, {{this_year}}
</a></h3>
<ul>
{% endif %}
<li style="list-style:none;padding:5px;">
<i class="fa fa-calendar"></i>
{{ post.date | date: "%Y-%m-%d" }}
<i class="fa fa-terminal"></i>
<a href="{{ post.url }}">{{ post.title }}</a></li>
{% if forloop.last %}
</ul>
{% else %}
{% if this_year != next_year %}
</ul>
<h2 style="text-align:center; background:#BFD9DB;">
<i class="fa fa-flag-checkered"></i>
<a href="#{{ post.previous.date | date: "%Y" }}" name="{{ post.previous.date | date: "%Y" }}">
{{ next_year }}
</a></h2>
<h3>
<i class="fa fa-calendar-check-o"></i>
<a href="#{{ post.previous.date | date: "%Y-%m" }}" name="{{ post.previous.date | date: "%Y-%m" }}">
{{next_month}}, {{next_year}}
</a></h3>
<ul>
{% else %}    
{% if this_month != next_month %}
</ul>
<h3>
<i class="fa fa-calendar-check-o"></i>
<a href="#{{ post.previous.date | date: "%Y-%m" }}" name="{{ post.previous.date | date: "%Y-%m" }}">
{{next_month}}, {{next_year}}
</a></h3>
<ul>
{% endif %}
{% endif %}
{% endif %}
{% endfor %}
</ul></div></div></section>
