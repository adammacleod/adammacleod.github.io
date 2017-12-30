---
layout: post
title: How to List Jekyll Posts by Category
categories: programming
tags: programming jekyll
hero: "/assets/images/code.jpg"
---

This post was <del>heavily inspired</del> more or less copied from Joe Kampschmidt's post [How to list your jekyll posts by tags](https://www.jokecamp.com/blog/listing-jekyll-posts-by-tag/). 

In his post, Joe shows how to create a list of posts sorted by the tags which they appear in. I wanted to achieve the same but instead listing by category rather than tag. I prefer categories as they are added into the URL when generating your site which I think is better for organisation (see [here](https://jekyllrb.com/docs/frontmatter/#predefined-variables-for-posts) for the differences).

{% highlight liquid %}
{% raw %}
  {% for category in site.categories %}
    {% assign category_name = category | first %}
    {% assign posts = category | last %}

    {{ category_name | capitalize }}
    <ul>
      {% for post in posts %}
        {% if post.categories contains category_name %}
          <li>
            <a href="{{ post.url }}">{{ post.title }}</a>
            <span class="date">{{ post.date | date: "%B, %Y"  }}</span>
          </li>
        {% endif %}
      {% endfor %}
    </ul>
  {% endfor %}
{% endraw %}
{% endhighlight %}