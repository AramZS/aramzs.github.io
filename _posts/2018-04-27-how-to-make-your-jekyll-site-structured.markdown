---
title: How to give your Jekyll Site Structured Data for Search with JSON-LD
date: 2018-04-27 22:00:51 Z
categories:
- jekyll
- schema-dot-org
layout: post
image: https://github.com/AramZS/aramzs.github.io/blob/master/_includes/beamdown.gif?raw=true
vertical: Code
excerpt: Let's make your Jekyll site work with Schema.org structured data and JSON-LD.
overlay: blue
hashtag: JekyllStructured
---

You've got Jekyll, now you need to get all your structured data ready for Google, archival systems and more with Schema.org markup. Here's how you can deploy a structured data in a JSON-LD format to your Jekyll site. 

A word of warning: this is a living document. Schema.org guidelines aren't set in stone and even if they were they suffer from bad documentation and frequently lack examples. If you're interested in some of the challenges I faced, I'll go into detail at the end of the article. If you want to know why this is worth the work even with these challenges, that is at the bottom as well. 

All the suggested code here validates in Google's [structured data checking tool](https://search.google.com/structured-data/testing-tool/u/0/). All work here is, to my best knowledge, correct and I welcome any [pull requests](https://github.com/AramZS/aramzs.github.io/pulls) to fix samples where I may have made a mistake.

## Ok let's get to the code!

The first thing we need to do is build support for managing JSON-LD in our templates. There's structured markup that can be done inline, using `itemprop`, `itemscope`, and `itemtype`, but we won't dive into those right now. We're just looking at the JSON-LD objects we can embed at page level that will tell any machine trying to understand our blog or blog posts important information about both the site and the post itself.

This lives in the HEAD, and we'll need different treatments for pages and posts then the home page. In `_includes/head.html` you'll need to check if you are in a page. I do this by checking page.title. I also wanted the capability to override any individual page's automatic JSON-LD with a manual setup. Here's how:

{% highlight html %}
{%raw%}

    <!-- Check to see if we are in a page. -->
    {% if page.title %}
        {% if page.jsonld %}
            {% include {{page.jsonld}}.html %}
        {% else %}
            {% include postJSONLD.html %}
        {% endif %}
    {% else %}
        {% include homeJSONLD.html %}
    {% endif %}  
</head>

{%endraw%}

{% endhighlight %}  

JSON-LD objects can become sizable to manage, and a bit of a pain to deal with when inside larger files. Here I make it simple by pulling the script for building JSON-LD out of the head.html file. I placed this code block at the end of the HEAD block, as illustrated by `</head>` at the bottom. Now one of three things will happen: 

1. If the page specifies a jsonld value, Jekyll will check to find that value as an HTML file in your `_includes` directory on page build. 
2. If the page does not specify a jsonld value, it will use the default file at `postJSONLD.html`.
3. If there is no title, we assume it's a site home page and use the `homeJSONLD.html` file.

All files will exist inside `_includes` and will be valid HTML. Note: you must create these files (and any custom files you specify) before you build your site or Jekyll will crash. If you (like I) are maintaining this on GitHub, that means before you `git push` to your repository.

First you'll want to set up your per-post JSON-LD file. We'll break down what's happening inside next.

{% highlight html %}
{%raw%}

<script type="application/ld+json">
    {
        "@context": "http://schema.org",
        "@type": "BlogPosting",
        "headline": "{{ page.title }}",
        "description": "{{ page.excerpt }}",
        "image": [
            {% if page.ogimageoff %}

            {% elsif page.ogimage %}
                "{{page.ogimage}}"
            {% elsif page.image %}
                "{{page.image}}"
            {% else %}
                "https://41.media.tumblr.com/709bb3c371b9924add351bfe3386e946/tumblr_nxdq8uFdx81qzocgko1_1280.jpg"
            {% endif %}
        ],
        "mainEntityOfPage": {
            "@type": "WebPage",
            "@id": "{{ page.url | replace:'index.html','' | prepend: site.baseurl | prepend: site.url }}"
        },
        "datePublished": "{{page.date}}",
        "dateModified": "{% if page.modified %}{{page.modified}}{% else %}{{page.date}}{% endif %}",
        "isAccessibleForFree": "True",
        "isPartOf": {
            "@type": ["CreativeWork", "Product", "Blog"],
            "name": "Fight With Tools",
            "productID": "aramzs.github.io"
        },
        "license": "http://creativecommons.org/licenses/by-sa/4.0/",
        "author": {
            "@type": "Person",
            "name": "Aram Zucker-Scharff",
            "description": "Aram Zucker-Scharff is Director for Ad Engineering at Washington Post, lead dev for PressForward and a consultant. Tech solutions for journo problems.",
            "sameAs": "http://aramzs.github.io/aramzs/",
            "image": {
                "@type": "ImageObject",
                "url": "https://pbs.twimg.com/profile_images/539484037765533698/7l6-pKY-_400x400.jpeg"
            },
            "givenName": "Aram",
            "familyName": "Zucker-Scharff",
            "alternateName": "AramZS",
            "publishingPrinciples": "http://aramzs.github.io/about/"
        },
        "publisher": {
            "@type": "Organization",
            "name": "Fight With Tools",
            "description": "A site discussing how to imagine, build, analyze and use cool code and web tools. Better websites, better stories, better developers. Technology won't save the world, but you can.",
            "sameAs": "http://aramzs.github.io",
            "logo": {
                "@type": "ImageObject",
                "url": "https://41.media.tumblr.com/709bb3c371b9924add351bfe3386e946/tumblr_nxdq8uFdx81qzocgko1_1280.jpg"
            },
            "publishingPrinciples": "http://aramzs.github.io/about/"
        }
    }
</script>

{%endraw%}

{% endhighlight %}  

To give some extra context, it's useful to see what the object for this post looks like.

{% highlight markdown %}
{%raw%}

---
layout: post
title:  "How to give your Jekyll Site Structured Data for Search with JSON-LD"
date:   2018-04-21 10:19:51 +0100
categories:  jekyll schema-dot-org
image: https://github.com/AramZS/aramzs.github.io/blob/master/_includes/beamdown.gif?raw=true
vertical: Code
excerpt: "Let's make your Jekyll site work with Schema.org structured data and JSON-LD."
overlay: blue
---

{%endraw%}

{% endhighlight %}  

Let's look at the top level object properties:
{% highlight json %}
{%raw%}

        "@context": "http://schema.org",
        "@type": "BlogPosting",
        "headline": "{{ page.title }}",
        "description": "{{ page.excerpt }}",
{%endraw%}

{% endhighlight %}  

The context property says we're using the Schema.org standard. The type describes what this page is - a blog posting. `headline` and `description` both take metadata about the post that exists in our markdown and places it properly in the schema format. 

{% highlight json %}
{%raw%}
        "image": [
            {% if page.ogimageoff %}

            {% elsif page.ogimage %}
                "{{page.ogimage}}"
            {% elsif page.image %}
                "{{page.image}}"
            {% else %}
                "https://41.media.tumblr.com/709bb3c371b9924add351bfe3386e946/tumblr_nxdq8uFdx81qzocgko1_1280.jpg"
            {% endif %}
        ],

{%endraw%}

{% endhighlight %}  

Here I've added a number of options to allow us to control the image in the JSON-LD statement, based on my [social media metadata setup](http://aramzs.github.io/jekyll/social-media/2015/11/11/be-social-with-jekyll.html). I'm checking here for `ogimageoff`: indicating no image, `ogimage`: an image intended specifically for social media and `image`: the preview image at the top of this page. If I've set nothing, I default to a standard image across my site. 

{% highlight json %}
{%raw%}
        "mainEntityOfPage": {
            "@type": "WebPage",
            "@id": "{{ page.url | replace:'index.html','' | prepend: site.baseurl | prepend: site.url }}"
        },
{%endraw%}

{% endhighlight %}  

This part is a bit unclear. Presumably we're already describing the mainEntityOfPage and this would not be required, but Google's tool requires it and Schema.org's demo, along with some news organizations, handles this property as type WebPage and gives it its own URL as an ID. 

{% highlight json %}
{%raw%}
        "datePublished": "{{page.date}}",
        "dateModified": "{% if page.modified %}{{page.modified}}{% else %}{{page.date}}{% endif %}",
        "isAccessibleForFree": "True",
        "isPartOf": {
            "@type": ["CreativeWork", "Product", "Blog"],
            "name": "Fight With Tools",
            "productID": "aramzs.github.io"
        },
        "license": "http://creativecommons.org/licenses/by-sa/4.0/",
{%endraw%}

{% endhighlight %}  

This block describes the date the content published, date it was modified and if it is behind a paywall (it is not). Because Google suggests `dateModified` no matter what the state, we check for a modified date and if none is set, we'll use the published date.

`isPartOf` describes this blog post as part of a larger object, the blog itself.

`license` provides a link to the Creative Commons license I have applied to this blog. 

{% highlight json %}
{%raw%}
        "author": {
            "@type": "Person",
            "name": "Aram Zucker-Scharff",
            "description": "Aram Zucker-Scharff is Director for Ad Engineering at Washington Post, lead dev for PressForward and a consultant. Tech solutions for journo problems.",
            "sameAs": "http://aramzs.github.io/aramzs/",
            "image": {
                "@type": "ImageObject",
                "url": "https://pbs.twimg.com/profile_images/539484037765533698/7l6-pKY-_400x400.jpeg"
            },
            "givenName": "Aram",
            "familyName": "Zucker-Scharff",
            "alternateName": "AramZS",
            "publishingPrinciples": "http://aramzs.github.io/about/"
        },
{%endraw%}

{% endhighlight %}  

The above is the author block, we establish a Schema.org standard `Person` object and provide data about it. In this case, the data is about me (since I'm the author). Most of the properties are self evident, but there are two important properties to examine. `publishingPrinciples` should link to a page that describes why and how you publish the way you do. `image` attaches an `ImageObject` to the Person object that is an image of me. `sameAs` links to a page that describes the same person object. It is on this site and we'll get into how that gets build later.

{% highlight json %}
{%raw%}
        "publisher": {
            "@type": "Organization",
            "name": "Fight With Tools",
            "description": "A site discussing how to imagine, build, analyze and use cool code and web tools. Better websites, better stories, better developers. Technology won't save the world, but you can.",
            "sameAs": "http://aramzs.github.io",
            "logo": {
                "@type": "ImageObject",
                "url": "https://41.media.tumblr.com/709bb3c371b9924add351bfe3386e946/tumblr_nxdq8uFdx81qzocgko1_1280.jpg"
            },
            "publishingPrinciples": "http://aramzs.github.io/about/"
        }
{%endraw%}

{% endhighlight %}

The final property describes the `publisher` object. In this case we're establishing it as this site, so the publishing organization for this post is this site. The properties within the object describes the site. 

That's the object! 

## Are you a person? Tell me how.

Now let's explore the process of establishing a `Person` object under a stand-alone URL and using the custom `jsonld` property of a `page`. 

At the base of the folder for this site, I've built a `whoami.md` file. This will be the new home of my Schema.org identity. It is topped with page data as follows:

{% highlight markdown %}
{%raw%}
---
layout: page
title: Who is Aram Zucker-Scharff?
navtitle: Who is Aram?
permalink: /aramzs/
excerpt: Aram Zucker-Scharff is Director for Ad Engineering at Washington Post, lead dev for PressForward and a consultant. Tech solutions for journo problems.
jsonld: jsonld-id
date: 2018-04-21 13:00:00 +0100
---
{%endraw%}

{% endhighlight %}

As you can see, I'm using the `jsonld` property to specify a stand-alone one-off `.html` file to use for the JSON-LD statement. Now I can create `_includes/jsonld-id.html`. Here's what that file looks like:

{% highlight html %}
{%raw%}
<script type="application/ld+json">
    {
        "@context": "http://schema.org",
        "@type": "Person",
        "name": "Aram Zucker-Scharff",
        "description": "{{ page.excerpt }}",
        "disambiguatingDescription": "A media-focused developer and strategist.",
        "image": [
            {% if page.ogimagenull %}

            {% elsif page.ogimage %}
                "{{page.ogimage}}"
            {% elsif page.image %}
                "{{page.image}}"
            {% else %}
                "https://pbs.twimg.com/profile_images/539484037765533698/7l6-pKY-_400x400.jpeg"
            {% endif %}
        ],
        "givenName": "Aram",
        "familyName": "Zucker-Scharff",
        "alternateName": "AramZS",
        "publishingPrinciples": "http://aramzs.github.io/about/"
    }
</script>
{%endraw%}

{% endhighlight %}

This object now lives at the top of [http://aramzs.github.io/aramzs/](http://aramzs.github.io/aramzs/). It means that page can now represent my identity as a Schema.org object *and* it can be referred to by other Schema.org objects as a Person. 

This is pretty cool because it now means I can refer to this on my site and on any site as a source of truth for my identity.

## Hello Blog

The final step at getting the Structure Markup for this blog as valid as possible is to describe the blog itself as an object. Most of that object is the same, the exception being my home page is a `Blog` object as opposed to a `BlogPosting`. Here's what it looks like:

{% highlight html %}
{%raw%}
<script type="application/ld+json">
    {
        "@context": "http://schema.org",
        "@type": "Blog",
        "url": "{{ prepend: site.baseurl | prepend: site.url }}",
        "headline": "{{ site.title }}",
        "about": "{{ site.description }}",
        "image": [
            "https://41.media.tumblr.com/709bb3c371b9924add351bfe3386e946/tumblr_nxdq8uFdx81qzocgko1_1280.jpg"
        ],
        "isAccessibleForFree": "True",
        "isPartOf": {
            "@type": ["CreativeWork", "Product"],
            "name": "Fight With Tools",
            "productID": "aramzs.github.io"
        },
        "discussionUrl": "https://twitter.com/search?f=tweets&vertical=default&q=to%3AChronotope&l=en&src=typd",
        "author": {
            "@type": "Person",
            "name": "Aram Zucker-Scharff",
            "description": "Aram Zucker-Scharff is Director for Ad Engineering at Washington Post, lead dev for PressForward and a consultant. Tech solutions for journo problems.",
            "sameAs": "http://aramzs.github.io/aramzs/",
            "image": {
                "@type": "ImageObject",
                "url": "https://pbs.twimg.com/profile_images/539484037765533698/7l6-pKY-_400x400.jpeg"
            },
            "givenName": "Aram",
            "familyName": "Zucker-Scharff",
            "alternateName": "AramZS",
            "publishingPrinciples": "http://aramzs.github.io/about/"
        },
        "editor": {
            "@type": "Person",
            "name": "Aram Zucker-Scharff",
            "description": "Aram Zucker-Scharff is Director for Ad Engineering at Washington Post, lead dev for PressForward and a consultant. Tech solutions for journo problems.",
            "sameAs": "http://aramzs.github.io/aramzs/",
            "image": {
                "@type": "ImageObject",
                "url": "https://pbs.twimg.com/profile_images/539484037765533698/7l6-pKY-_400x400.jpeg"
            },
            "givenName": "Aram",
            "familyName": "Zucker-Scharff",
            "alternateName": "AramZS",
            "publishingPrinciples": "http://aramzs.github.io/about/"
        },
        "inLanguage": "en-US",
        "license": "http://creativecommons.org/licenses/by-sa/4.0/",
        "additionalType": "CreativeWork",
        "alternateName": "Fight With Tools",
        "publisher": {
            "@type": "Organization",
            "name": "Fight With Tools",
            "description": "A site discussing how to imagine, build, analyze and use cool code and web tools. Better websites, better stories, better developers. Technology won't save the world, but you can.",
            "sameAs": "http://aramzs.github.io",
            "logo": {
                "@type": "ImageObject",
                "url": "https://41.media.tumblr.com/709bb3c371b9924add351bfe3386e946/tumblr_nxdq8uFdx81qzocgko1_1280.jpg"
            },
            "publishingPrinciples": "http://aramzs.github.io/about/"
        }
    }
</script>
{%endraw%}

{% endhighlight %}

I added a property to describe an `editor`. It's just me here, but if someone else edits your work regularly, you could include there here. You could even do so on a per-post level. I also [linked to a search on Twitter](https://twitter.com/search?f=tweets&vertical=default&q=to%3AChronotope&l=en&src=typd) for people directing tweets to me as the `discussionUrl` for this blog. 


You can check out the code I walked through here [in the repository for this blog](https://github.com/AramZS/aramzs.github.io/blob/master/_includes/postJSONLD.html). 

### Challenges

Schema.org still has not been implemented across the web and so we frequently lack examples in the wild, and where they are live they can be inconsistent or conflict with other sites' interpretations of the rules. The examples on the Schema.org site do not cover every case and even where they do, they don't always make sense. 

Because of this issue, there isn't a clear answer to the question of how these JSON-LD objects should be formed, especially when dealing with specific situation or pages-as-objects (which is the intent of the JSON-LD head-level data). A good example of this is `mainEntityOfPage`. Theoretically you use this to designate the primary 'object' of the page, but isn't that exactly the intent of the entire JSON-LD object? I'm not sure. 

The other challenge is that you can get your structured data object correct but apply it to the wrong page, misrepresenting the object. There's no real way to check this and extensive examples are hard to find.

### Why bother?

With the complexity and lack of clarity involved in JSON-LD, why should you add it to your Jekyll site?

A bunch of reasons! Structured data is important for getting the best chance at topping a Google Search page. That might be reason enough for you. That isn't the only reason: 

 - It's important for systems that attempt to understand and archive the web. 
 - These data structures are useful for voice-controlled systems that might want to use data from your site.
 - Like OpenGraph's less complex data, JSON-LD data is vital for the [Semantic Web](https://www.w3.org/RDF/Metalog/docs/sw-easy) and allows computers and humans to better work together.

Thanks for making it to the bottom! JSON-LD and Structured Data is important to the future of the web and I hope this article makes implementing it on your Jekyll site easier!.

#### \*Developer Testing Note!

Frustrated by trying to set up your JSON-LD locally and being unable to test it? I used `bundle exec jekyll serve --incremental` to set up my Jekyll site as a local server on port `4000` and then used a CLI application called [Ngrok](https://ngrok.com/) `ngrok http 4000` to make my local server visible publicly so I could check it with the Google Structured Data Testing tool.
          