---
layout: post
title:  "Add Post Featured Images with Liquid"
categories: site-building
tags: liquid
# image_url: fds
---

I found a [video online](https://www.youtube.com/watch?v=6oKO-7gsM4s&list=LL&index=1) explaining how to add featured images to Jekyll posts using liquid. I followed the instructions but I needed to extend the code for especial cases. In this post I explain what I added. 

My idea was to add another front matter variable for the feature image source link. This is a simple task if we assume that we will only get one source link per post.

The featured image in my [first post]({% post_url 2022-12-18-mood-board %}), a mood board, required multiple links (it is composed of multiple images). This seemed a great opportunity to practice some liquid language so here is what I did:

In every post's front matter I assign the source of the image to a variable <code>image_url</code>. If the image has only one source then the variable will be a string containing that information.

{% highlight YAML %}
# 2022-12-18-my-post-title.markdown
---
image_url: https://unsplash.com/photos/Adl90-aXYwA
---
{% endhighlight %}

If the image refers to multiple sources then the <code>image_url</code> variable will be an array containing all the sources:

{% highlight YAML %}
# 2022-12-18-my-post-title.markdown
---
image_url: 
  - https://unsplash.com/photos/Adl90-aXYwA
  - https://unsplash.com/photos/4QVoKxlnsx0
  - https://unsplash.com/photos/asYCpxbYTWc
---
{% endhighlight %}

In liquid, we can [use the array filter "first"](https://stackoverflow.com/questions/38917552/check-if-variable-is-type-of-string-or-array-in-liquid) to check if a variable is a string or a list of elements. This way, when <code>image_url</code> is an array I use a loop for displaying the links to the sources with numbers using <code>forloop.index</code>.

{% highlight html %}
{% raw %}
<!-- post.html -->
{%- if page.image -%}
    <img src="{{- page.image | relative_url -}}" alt="" class="featured-image-post">
    {%- if page.image_url.first -%}
      {% comment %} multiple urls provided! {% endcomment %}
      <p>
        (Picture sources: 
        {% for url in page.image_url %}   
          {%- if forloop.last -%}
            <a href="{{url}}">{{forloop.index}}</a>
          {%- else -%}
            <a href="{{url}}">{{forloop.index}}</a>,&nbsp;
          {%- endif -%}
        {%- endfor -%}
        )
      </p>
      {%- else -%}
        {% comment %} one url only {% endcomment %}
        (Picture: {{page.image_url}})
    {%- endif -%}
{%- else -%}
    {%- assign postImage="/assets/images/image-default.jpg" -%}    
    <img src="{{- postImage | relative_url -}}" alt="" class="featured-image-post">
    <p>(Picture: https://unsplash.com/photos/cckf4TsHAuw)</p>
{%- endif -%}    
{% endraw %}
{% endhighlight %}

This solution works for me for now. I am learning jekyll and liquid as I move forward, so there might be a better approach that I am not aware of - I will post a better solution in the future if I find one.