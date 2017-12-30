---
layout: post
title: Dynamic Header Images Using YAML Front Matter in Jekyll
category: programming
tags: programming jekyll css
hero: "/assets/images/code.jpg"
---

Recently I wanted to dynamically update my site banner image in Jekyll based on which page I was viewing. It turns out that this is surprisingly easy without needing to resort to any dynamic javascript (yay for static site compilers).

### Set a default background-image in your CSS file

This was the CSS I used before I had a dynamic hero image, there's nothing too special here - by doing this we can default to the sitewide image if a specific one isn't provided within the [front matter](https://jekyllrb.com/docs/frontmatter/).

{% highlight scss %}

.site-banner {
  background-image: url("/assets/images/office.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center left;
  min-height: 550px;
}

{% endhighlight %}

### Update your CSS inline based on the YAML front matter

While it would be preferable to localise this change entirely to the CSS file there are [reasons](https://github.com/jekyll/jekyll/issues/2573) (for better or worse) why jekyll doesn't process liquid tags within the assets folder. Thus, into the HTML we must go. As shown below, we optionally include an inline style tag which sets our background-image.

{% highlight liquid %}
{% raw %}

<header 
  class="site-banner" 
  {% if page.hero %} 
    style="background-image: url('{{ page.hero }}')" 
  {% endif %}>
</header>

{% endraw %}
{% endhighlight %}

This wouldn't work in a modern single page application (SPA) but it works here because Jekyll processes all of the assets for each page that it generates.

### Set a custom image within your post's front matter

Now, we can easily set the ```hero``` variable within our front matter to dynamically set the header image. The background image will safely revert to our site default for pages where we don't set the hero variable in the front matter. There are two examples below showing the hero variable in action:

#### Using an absolute path

{% highlight yaml %}
{% raw %}

---
layout: post
title: Dynamic Header Images Using YAML Front Matter in Jekyll
category: programming
tags: programming jekyll css
hero: "/assets/images/code.jpg"
---

{% endraw %}
{% endhighlight %}

#### Using an external web server (not recommended)

{% highlight yaml %}
{% raw %}

---
layout: post
title: Dynamic Header Images Using YAML Front Matter in Jekyll
category: programming
tags: programming jekyll css
hero: "https://jekyllrb.com/img/logo-2x.png"
---

{% endraw %}
{% endhighlight %}