---
layout: post
title:  "Day of REST Notes"
date:   2017-03-09 10:34:51 -0500
categories: tools wordpress api
vertical: Code
excerpt: "Day of REST #feelingRESTful"
---

Add links to your response `_links` `link type`: `/wp/v2/etc...` which can then be added to the API base to get more data through that link.

If embeddable then you can add `?_embed` to the end.

You can use `enum` on something like status to list the potential things that a schema provides. (See post status.)

Different Authentication methods are available and new ones are plugable. The basic support is cookie based, basic auth, oauth 1 and brokered auth.

`wp.api` is automatically loaded inside wordpress for using the API. It uses cookie authentication out of the box.

Basic Auth is the type your browser uses, not very secure, browser pops up and data is sent in plain text.

When connecting from one site to another, OAuth is the recommended approach.

OAuth 2 is a little more limited in scope b/c it requires HTTPS.

== OAuth 1
 - Install the REST API OAuth 1.0 plugin
 - Create a new app in the WordPress Dashboard.
 - Continue with the OAuth 1.0 flow
 - oauth1.wp-api.org.

The steps for a user are quite arduous, they have to create an app and authorize it.

The solution for this difficult project is Brokered Authentication.

== Brokered Authentication
 - Register at apps.wp-api.org
 - The App that you are building, the WordPress site you want to use, the apps broker.
 - The app contacts the broker.
 - The broker contacts the site
 - The broker than forwards the key to the app.
 - apps.wp-api.org/spec
 - apps.wp-api.org/app-developers

 Client Libraries are a major part of the process.
  - Backbone Core Client - `wp_enqueue_script('wp-api')`
   - gives you the `wp.api` object for access.
  - `npm install wordpress-rest-api-oauth-1`
  - wpapi NodeJS/Browser - for use in a client or Browser
   - `npm install wpapi`

== Developing
 - `register_meta`
 - `register_settings`
 - `register_rest_field`
 - You can use the WP_REST_Controller to create totally new methods.

= API Tales of Woe and Woah

If you use GET for destructive actions then suddenly Google's crawler can start
deleting stuff. Use PATCH/DELETE or at least POST for destructive actions.

Don't mess with the internet's conventions.

Don't do Slow Stuff - don't make the user wait for slow stuff to happen, async as much as possible.

But also check to make sure your async code is actually quicker.

Defensive routing
 - Support trailing slashes but only as looking for something you're meant to be looking for.
 - So `/foo/` maybe should deliver a 404 but `/foo` should deliver the first page of foos.
 - Be error heavy
 - Apply limits.
 - Apply pagination.
 - Apply pagination limits, an upper and lower bound (don't let people request -1 page)

Includes are cool, but restrict what people can include.

Easy win - use SSL - now with letsencrypt.org it is free.

Universal Uniqueness
 - Avoid people downloading your entire dataset and putting you out of business.
 - UUIDs stop slow and malicious downloading of your public but unique data.
 - Don't let people illegally download all your data, or at least detect it.
 - UUID performance tweaks exist.

Runscope useful for testing APIs.

Errors should throw useful and HTTP error codes. Don't have your error pages 200.
 - This is useful for tracking systems like Runscope or New Relic.

REST has nothing to do with returning status codes properly, you should always be doing that.

Return things that make sense to both a computer and a human.

Put a link to the documentation in your error!

Retry failures from the client side.
 - If a request gets a server timeout, try it again.
 - Maybe try it twice, but wait a second or two
 - Check the status code, anything 500 error can usually be retried.

`hello.js` is a package for logging into an OAuth.

429 usually means rate limit exceeded, except Google sends a 403.

"Google is not really helping out when they ignore the conventions"

HTTP Status Cats.

Don't retry on all failures. If you go over the rate limiting pop a 429 error that maybe has a Retry-After header to tell you when you should be retrying.

It is more important to give useful feedback to your clients.

Don't cache errors! (Don't let Varnish cache your 429 errors)

By default 404 gets cached on Varnish, which can cause trouble for things like API requests.
 - For 10 minutes a thing might not exist in your app at all, with the default Varnish configuration.
 - If the status code is X set the time to live (ttl) lower, like to 0 or your Retry-After?

 Expect the worst from everyone.

If it is not JSON - catch that exception!

Also catch HTTP server errors when you can!

The response might be empty if it is a timeout. Check for that.

Never assume the shape of the data, check for it and throw an error when it returns an unexpected shape.

Documentation is important - Swagger, Ramble(sp?), etc... JSON Schema

Stop services from lying to each other
 - [Strong Parameters](packagist.org/packages/koine/strong-parameters)
 - PHP-VCR instead of static stubs
 - Be sure to re-record VCR stubs
 - Jenkins can host entire stack with Docker Compose.
 - Set up with Travis as well is possible.

Build APIs You Won't Hate - apisyouwonthate.com


[party stats at 6pm]

post status club discount adayofrestboston
