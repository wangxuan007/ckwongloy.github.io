---
layout: blog_backbone
title: Category @ckwongloy
---

<a href="" name="top"></a>

<section class="main-content" style="font-family:Georgia;">
<div class="home">
<h3 class="page-heading">
<strong>
<a href="/home/" title="Bak to Home">
<i class="fa fa-home"> Home</i></a>
<i class="fa fa-angle-double-right" style="color:silver;"></i>
<i class="fa fa-folder"> Category</i>
<i class="fa fa-terminal" style="color:red;"></i></strong></h3>

<h2 style="text-align:center;">
<i class="fa fa-bolt"></i>
<i class="fa fa-bolt"></i>
<i class="fa fa-bolt"></i>
Full-Stacking
&times;

{{ site.categories | size }}

</h2>

<div style="background: #F7F6F6;">

{% for category in site.categories %}

<p style="font-size:24px;margin-left:5%;">
<i class="fa fa-folder"></i>
<a href="#{{ category | first }}" title="view all posts in &lt;{{ category | first }}&gt;">

{{ category | first }}

</a>
<i class="fa fa-angle-left"></i>

{{ category | last | size }}

<i class="fa fa-angle-right"></i></p>

{% endfor %}

</div>
<h2 style="text-align:center;">
<i class="fa fa-bolt"></i>
<i class="fa fa-bolt"></i>
<i class="fa fa-bolt"></i>
<strong>
Details
</strong></h2>

{% for category in site.categories %}

<p style="font-size:24px;margin-left:5%;">

<i class="fa fa-folder-open"></i>

<a href="#{{ category | first }}" name="{{ category | first }}" title="view all posts in &lt;{{ category | first }}&gt;">

{{ category | first }}

</a>
<i class="fa fa-angle-left"></i>

{{ category | last | size }}

<i class="fa fa-angle-right"></i></p>
<ul>

{% for post in category.last %}

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
