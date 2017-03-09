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

[party stats at 6pm]

post status club discount adayofrestboston
