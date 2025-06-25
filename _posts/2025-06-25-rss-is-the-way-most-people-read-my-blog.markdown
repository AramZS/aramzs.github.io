---
title: Here's how I know that more people read my personal blog via RSS then any other
  platform
date: 2025-06-25 14:30:00 -04:00
categories:
- open-source
tags:
- code
- rss
- analytics
- metrics
- privacy
vertical: Code
image: https://github.com/AramZS/aramzs.github.io/blob/master/_includes/rss-zs-favicon-2400-1200.png?raw=true
hashtag: RSSLives
excerpt: I am very happy to find out that more people read my blog on RSS than anywhere
  else, but how to figure that out and technically measure RSS readers proved difficult.
overlay: orange
toc: false
---

I want people to read my RSS feeds. but I also want to know how what my RSS readership is without breaching their privacy. RSS feed readership measurement is an... imperfect affair. Because it is a service that people generally charge for (or [require you to give up audience data for](https://feedburner.google.com/)) it isn't well documented. Here's how I did it.

I'm a big proponent of setting up fast, small, flat websites on the cheap. That means using free hosting and building services as much as possible. The goal [is to put the tools for crafting the web in the hands of as many people as possible](https://aramzs.github.io/build-a-website/#/).

RSS feeds present a set of unique problems for measurement which is why many companies, including big ones, don't do much to try and measure them.

The first big problem is that the big RSS readers cache your feed so they don't have to ping it constantly. This means that requests to your RSS feed URLs aren't really representative of the amount of readers you have.

Also a lot of RSS readers will cache the *inside* of the feed, so not just text but images will often get baked into the caching of a reader so that more complex reading applications don't have to over-request your site. This is one of the big challenges of measuring podcast downloads as well, iTunes and Spotify will absolutely save local copies of your file and only the introduction [of an intermediary service capable of authoring agreements with all the major players](https://analytics.podtrac.com/) have kept podcast measurement fairly reliable and kept all entities involved agreeing on the same numbers.

As far as I can tell, only Feedburner came close to being the Podtrac of text RSS feeds and since then, no one has really emerged as the one true agreed upon analytics provider for feeds that feed services will ping. I think that's good actually. *One True* services are generally a recipe for disaster.

By an apparent unwritten agreement, [major feed services will tell you about the readership of your feed in the header of their requests apparently, this is visible in server logs as Darek Kay discovered in 2021](https://darekkay.com/blog/rss-subscriber-count/). Though this isn't particularly standardized (requests don't seem to share a format) it seems useful... **if you can get your server's logged requests and generate reports based on them**.

If you are building fast, cheap, free-hosted sites like mine however, that is not an option. Also, I'm too lazy to futz around in server logs right now, even if I had them at hand.

So I wanted to try some stuff. I tried sending up an SVG that had analytics embedded in it. That did not work. I didn't bother with an old time pixel since I knew that trying to have an image on a server whose logs I did control wasn't the solution I wanted, even if it worked.

Instead I looked at the feeds I read and realized something.

There are videos in there. All those videos are handled like modern videos mostly are, embeds via iframes.

Now, iframes are not technically allowed in feeds, but the modern blog will tend to use them a lot for stuff like video, social media embeds, etc... anyway and it looks to me like most feedreaders will render them!

This is great! Now I can deploy an iframe and a page with analytics running on it and see if it works and... it does!

So I put together an HTML page:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Private Feed Tracker</title>
	<style>
		  * {
			box-sizing: border-box;
		  }

		  body {
			margin: 0;
			padding: 0;
			overflow: hidden;
			background: #03092c;
		  }

		 img {
			margin: 0 auto;
			display: block;
			padding: 0;
		 }
	</style>
	<script data-domain="aramzs.xyz" src="https://plausible.io/js/plausible.js"></script>
  </head>
  <body>
	<!-- Hi! This image is loaded in an iframe on my RSS feed as a way to try and measure how many people are reading me through RSS. The tracking is privacy respecting and your data will not be sold. I'm just curious.  -->
	<img src="/feed-img.svg" width="50" height="50" alt="Site logo">
  </body>
</html>
```

As you can see, I've created a standalone HTML page on [my personal blog site](https://aramzs.xyz/) that includes a simple call to my privacy-focused analytics provider Plausible.

Then my RSS NJK template gets the iframe that loads this file added to the end of every article's content block:

```liquid
set postContent = post.templateContent + '<br></br><iframe width="50" height="50" src="/some-url-with-that-html" title="Privacy-respecting tracker for feed readers" frameborder="0" allow="web-share" referrerpolicy="strict-origin-when-cross-origin"></iframe>' | htmlToAbsoluteUrls(absolutePostUrl)
```

And yeah, this works! Now maybe some services cache iFrames as well, and so what I'm really getting isn't my full readership but a baseline of minimum-measurable-readers. This is very possible, but even the baseline is an exciting number to be able to get access to without enlisting anything other than my normal analytics provider!

It's possible they're getting pre-loaded in some contexts; but I suspect most applications won't load iframes in a post until the post is opened by the user. It is also possible that this is **only** getting loaded *because it is a visible image*, but I didn't test out a 1x1 version to verify. I didn't want to seem sneaky here, I want to make it obvious that an asset is loading from my site.

I think this is a pretty reasonable number to work with!

And look at my past 28 days! It turns out that I am getting more traffic on my RSS posts than on any other individual page.

![Overall stats of pageviews per page on my site](/uploads/rss-stats-in-context.png)

And when I break it out as a source it constitutes over a third of my traffic.

![Stats on RSS as a standalone source](/uploads/rss-stats.png)

This is super exciting to me! I want people to consume the two RSS feeds I produce for [aramzs.xyz](https://aramzs.xyz). It looks like they are!

## Some Interesting Information

I specifically use Plausible as my analytics provider because it is non-invasive, quick, and privacy preserving. I don't want detailed user data, or even anything other than the most generic data about users. But I do like having referrer data and when I looked at Top Sources I was surprised to see a whole bunch of sites.

I am not sure what exactly is happening there, or how to figure out more information with my current setup, but I assume some of these are people flowing from those sites into my RSS feed when their browser has something that renders the feed directly. The presence of [Inoreader](https://www.inoreader.com/) makes me realize that readers will also show up as referrers in this process. I think this means that a bunch of these sites are running their own white-labeled in-house RSS readers for their employees or users, which is really cool!

## What is next?

I have two RSS feeds for two very different purposes, one supplies my own writing, the other is an amplifeed of articles I want to amplify (like a retweet!). I might give those two different iFrames to see how the different feeds perform separately.

I would also like to know which specific articles are getting loaded by readers, it would be nice to combine into my metrics, but I just don't think that's possible with my current setup. What I might try is some link-decoration to track the article names/urls as setting up alternative URLs is just not desirable. I'll have to see if that works or causes issues (since I know some applications and browsers will intercede against or strip out link decoration).

If you've tried this or have had some experience with this sort of thing, [hit me up on BlueSky](https://chronotope.aramzs.xyz/).
