---
title: How to make your Jekyll site show up on social
date: 2015-11-11 15:34:51 Z
categories:
- jekyll
- social-media
layout: post
image: https://raw.githubusercontent.com/AramZS/aramzs.github.io/master/_includes/tumblr_nwncf1T2ht1rl195mo1_1280.jpg
vertical: Code
excerpt: Here's how to make Jekyll posts easier for others to see and share on social
  networks.
---

Congratulations, you've set up a Jekyll site. You may even be, like me, taking advantage of the free hosting provided by GitHub. You've written your first post, you've set up all the options. But when you go to share it on Facebook, Tumblr, LinkedIn or Twitter, that share may not look so pretty.

Here's how to make Jekyll posts easier for others to see and share on social networks.

To fix ugly shares and be the envy of all your GitHub followers you'll have to add some metadata to the HTML `HEAD` tag. Following is a walk-through of what tags and Liquid code is needed to generate those tags. Unless otherwise indicated, this markup goes in the `head.html` file in your `_includes` folder. If you're not already familiar with social and open graph tags, this post should be a useful illustration of how they work.

First, there are standard tags that should be applied on every page.

{% highlight html %}
{%raw%}

<!-- The Author meta propagates the byline in a number of social networks -->
<meta name="author" content="Aram Zucker-Scharff" />

{%endraw%}


{% endhighlight %}  

The `og:title` tag sets the title for sharing. I've duplicated the logic of the title tag to show either the site title or the post title based on what location the user has loaded. You could set a post-level variable for custom title as well or change the number of allowed characters.

We'll do the same with duplicating the logic of the `description` to `og:description` and `canonical` to `og:url` tags.

I've made the below Liquid statements multi-line for easier reading, but I wouldn't recommend that in production.

{% highlight html %}
{%raw%}


<meta property="og:title"
    content="{% if page.title %}
      {{ page.title | strip_html | strip_newlines | truncate: 160 }}
    {% else %}
      {{ site.title }}
    {% endif %}">

<meta property="og:description"
    content="{% if page.excerpt %}
        {{ page.excerpt | strip_html | strip_newlines | truncate: 160 }}
      {% else %}
        {{ site.description }}
      {% endif %}">


<meta property="og:url"
    content="{{ page.url | replace:'index.html','' | prepend: site.baseurl | prepend: site.url }}" />

  {%endraw%}
{% endhighlight %}  

Populating the Open Graph site name and locale tags is fairly straightforward.

{% highlight html %}
{%raw%}

<meta property="og:site_name" content="{{ site.title }}" />

<meta property="og:locale" content="en_US" />

  {%endraw%}
{% endhighlight %}  

These are the site-wide Twitter tags. My `twitter:site` property is set to my personal name, but you might want to set it to your site's account, if you have one. Description is set to the same data as the other description tags.

{% highlight html %}
{%raw%}


<meta name="twitter:site" content="@chronotope" />
<meta name="twitter:description" content="{% if page.excerpt %}{{ page.excerpt | strip_html | strip_newlines | truncate: 160 }}{% else %}{{ site.description }}{% endif %}" />

  {%endraw%}
{% endhighlight %}  

To populate all the fields social networks expect, you'll need some extra properties on your posts. Here's what the head of this post's markdown file looks like.

{% highlight html %}
{%raw%}


---
layout: post
title:  "How to make your Jekyll site more shareable"
date:   2015-10-29 01:34:51 -0400
categories: jekyll social-media
image: http://41.media.tumblr.com/173cb5c51a1c308ab022a786f69353f3/tumblr_nwncf1T2ht1rl195mo1_1280.jpg
vertical: Code
excerpt: "Jekyll is pretty cool, here's how to make writing with it easier for others to share on social networks."
---


{%endraw%}


{% endhighlight %}

There are a number of meta tags that are either site or article only. In order to figure out if we're on an article or not Liquid can switch in an if/else statement on the page.title.

{% highlight html %}
{%raw%}


{% if page.title %}
  <!-- Article specific OG data -->
  <!-- The OG:Type dictates a number of other tags on posts. -->
  <meta property="og:type" content="article" />
  <meta property="article:published_time" content="{{page.date}}" />

  <!-- page.modified isn't a natural Jekyll property, but it can be added. -->
  {% if page.modified %}
    <meta property="article:modified_time" content="{{page.modified}}" />
  {% endif %}

  <!-- Here my author and publisher tags are the same (yay self-publishing) -->
  <meta property="article:author" content="http://facebook.com/aramzs" />
  <!-- But if your site has its own page, this is where to put it. -->
  <meta property="article:publisher" content="https://www.facebook.com/aramzs" />

  <!-- Article section isn't a required property, but it can be good to have -->
  <meta property="article:section" content="{{page.vertical}}" />

  <!-- I use the page.categories property for OG tags. -->
  {% for tag in page.categories %}
    <meta property="article:tag" content="{{tag}}" />
  {% endfor %}

  <!-- I prefer the summary_large_image Twitter card for posts. -->
  <meta name="twitter:card" content="summary_large_image" />
  <!-- You, you're the creator. -->
  <meta name="twitter:creator" content="@chronotope" />
  <!-- This property is for the article title, not site title. -->
  <meta name="twitter:title" content="{{page.title}}" />

  {%endraw%}
{% endhighlight %}

Sharing works better with pictures. You can upload them to your repository, or link them from other locations. Not every page may have an image, so I've built a check to assure that an image has been supplied. If one hasn't, it returns to the default image I have for the whole site.

This takes care of both the Open Graph and Twitter Image tags. With more page properties you could have custom images for each if you wanted.

{% highlight html %}
{%raw%}

  {% if page.image %}
    <meta property="og:image" content="{{page.image}}" />
    <meta name="twitter:image" content="{{page.image}}" />
  {% else %}
    <meta property="og:image" content="https://41.media.tumblr.com/709bb3c371b9924add351bfe3386e946/tumblr_nxdq8uFdx81qzocgko1_1280.jpg" />
    <meta name="twitter:image" content="https://41.media.tumblr.com/709bb3c371b9924add351bfe3386e946/tumblr_nxdq8uFdx81qzocgko1_1280.jpg" />
  {% endif %}

  {%endraw%}
{% endhighlight %}

What if you're not on a post page? There are some default values we can fill in to indicate that we're on the basic website.

{% highlight html %}
{%raw%}

{% else %}
  <!-- OG data for homepage -->
  <meta property="og:image" content="https://41.media.tumblr.com/709bb3c371b9924add351bfe3386e946/tumblr_nxdq8uFdx81qzocgko1_1280.jpg" />
  <meta property="og:type" content="website" />
  <meta name="twitter:card" content="summary" />
  <meta name="twitter:title" content="{{site.title}}" />
  <meta name="twitter:image" content="https://41.media.tumblr.com/709bb3c371b9924add351bfe3386e946/tumblr_nxdq8uFdx81qzocgko1_1280.jpg" />

{% endif %}

  {%endraw%}
{% endhighlight %}

That's all of them! If you're interested, you can see the whole set of tags, the Liquid script, and the rest of `head.html` that I use for this very site by [checking the repo][repo-head].

[repo-head]: https://github.com/AramZS/aramzs.github.io/blob/master/_includes/head.html
