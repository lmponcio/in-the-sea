---
layout: post
title:  "Category Pages in Jekyll"
categories: updates
tags: jekyll liquid html
# image: assets/images/2022-12-26-theme-change.jpg
---

The webpage will have three categories: "Website Updates" (like this post), "Coder Talks" and "Tutorials". Links to two of them will be available in the nav bar.

I learned to access the posts belonging to a category from [this example](https://blog.webjeda.com/jekyll-categories/), and I used the [Home page]({{ "/" | relative_url }}) layout posts list as a guide for creating the page.

{% highlight html %}
{% raw %}
<!-- updates.html -->
<!-- ... -->
<div>
<ul class="post-list">
  {%- for post in site.categories["updates"] -%}
  <li>
    {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
    <span class="post-meta">{{ post.date | date: date_format }}</span>
    <h3>
      <a class="post-link" href="{{ post.url | relative_url }}">
        {{ post.title | escape }}
      </a>
    </h3>
    {%- if site.show_excerpts -%}
      {{ post.excerpt }}
    {%- endif -%}
  </li>
  {%- endfor -%}
</ul>
</div>
{% endraw %}
{% endhighlight %}

Later I realized I needed a way to distinguish between a category page that shows in navigation bar and one that doesn't. [This post](https://www.tahirtaous.com/exclude-pages-jekyll-navigation-menu-minima-theme/) explains a way of achiving it by combining a front matter variable (`exclude`) in the category page, and using the [unless](https://shopify.dev/api/liquid/tags#unless) liquid tag in the header file.


{% highlight html %}
{% raw %}
<!-- updates.html -->
---
layout: page
permalink: /updates/
title: Website Updates
exclude: true # for it not to show in nav
---
<!-- ... -->
{% endraw %}
{% endhighlight %}

{% highlight html %}
{% raw %}
<!-- header.html -->
<!-- ... -->
<div class="trigger">
{%- for path in page_paths -%}
    {%- assign my_page = site.pages | where: "path", path | first -%}
    {%- unless my_page.exclude -%}
        {%- if my_page.title -%}
        <a class="page-link" href="{{ my_page.url | relative_url }}">{{ my_page.title | escape }}</a>
        {%- endif -%}
    {%- endunless -%}
{%- endfor -%}
</div>
<!-- ... -->
{% endraw %}
{% endhighlight %}

The last thing I did was to apply a [reverse](https://shopify.dev/api/liquid/filters#reverse) tag to the list of pages for the About to be on the right. I like this solution for now because it is very simple - if the amount of pages in nav grow I might have to apply a different solution. 
{% highlight html %}
{% raw %}
<!-- header.html -->
<!-- ... -->
{%- assign page_paths = site.header_pages | default: default_paths | reverse -%}
<!-- ... -->
{% endraw %}
{% endhighlight %}