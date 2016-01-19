---
layout: post
title:  "How to get a React project linting in real time with Atom"
date:   2016-01-18 10:34:51 -0400
categories: React, JSHint
vertical: Code
excerpt: "A very very quick how to."
---

First install the JSHint package for Atom.

At the base of your project you'll need a `.jshintrc` file. It should enable ES6.

{% highlight js %}
{%raw%}

{
	"esversion" : 6
}

{%endraw%}
{% endhighlight %}  

Then under `Atom -> Open Your Config` add the following:

{% highlight json %}
{%raw%}

jshint:
  supportLintingJsx: true

{%endraw%}
{% endhighlight %}  
