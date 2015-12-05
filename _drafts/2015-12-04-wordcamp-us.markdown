---
layout: post
title:  "WordCamp US Notes"
date:   2015-12-04 09:34:51 -0400
categories: notes wordpress wordpressus2015
image: https://2015.us.wordcamp.org/files/2015/09/bg1-2x.jpg
vertical: Code
excerpt: "Notes!"
---

#WiFi

WordCampUS : opensource

## Friday

# First Lightning Talk - Project Management in WordPress with Sarah Pressler (@sarahpressler)

 - Team Leadership
 - "If you can handle being yelled at, you'll probably make a good project manager."

# Second Lightning Talk - [The Techie Continuum][techie-continuum] - Kathryn Presner

 - Do I know enough? A question many of us ask ourselves.
 - "I'm not a techie" but I share tech knowledge and people come to me for tech advices.
 - Nightmare - fired before hired.
 - Dwell on your praise - at Automattic, they get hugs from customers and send compliments to each other internally.
 - Don't be afraid to share your knowledge.

# Session 2 - [Developers Toolbox][dev-tools] - Tracy Rotton (@taupecat)

 - [Slides][http://taupecat.github.io/wordpress-toolbox]
 - Revision control is very important, Git is the way to go.
	  - There are alternatives to Git, WordPress has used Subversion for a long time but is slowly switching to git.
	  - Repository options: GitHub, Beanstalk, Atlassian Bitbucket, AWS CodeCommit
 - `define( 'DISALLOW_FILE_EDIT', true );` - Set this up so no changes can be done outside of git revisions.
 - Vagrant
	  - A computer inside your computer.
	  - Can be configured with code.
	  - Allows for closer match with the production environment.
	  - Environments can be created or destroyed at will.
	  - Good starter Vagrant for WP development - [Varying Vagrant Vagrants][vvv]
 - Package Managers
	  - [Composer][composer] - package manager for PHP
	  - [NPM][npm] - we're using it to install more libraries!
	  - [Bower][bower] - We're using it to install Sass libraries, [FontAwesome][fontawesome]
	  - Don't forget that a number of packages come with WordPress and you don't need to install them.
 - Javascript task runners
	  - Convert Sass
	  - Check your Javascript for errors
	  - Deploy to AWS
	  - [Gulp][gulp] vs [Grunt][grunt]
		   - Gulp has more complexity available.
		   - Also Brunch and Broccoli in the third tier
 - [WP-CLI][wpcli]
    - Anything you can do on the commandline you can script.
 - ["\_s"][s]
    - Starter theme for WordPress
    - Takes care of a lot of basics.
 - [WordPress Plugin Boilerplate][plugin-boilerplate]
    - Blank scaffold of Plugin best practices.
 - What belongs in my theme and what belongs in a custom plugin?
 - Plugin tools
	- [Show Template][show-template-plugin]
	- [Theme Check][theme-check-plugin]
	- [Debug Bar][debug-bar-plugin]
	- [Regenerate Thumbnails][regenerate-thumbnails-plugin]
	- [WP Migrate DB (PRO)][migrate-db-plugin]
 - Invest the time in the beginning of a project to put good tools into place ... [things] will go a lot more smoothly.
 - "I don't commit compiled javascript"
	- Repositories are only for code that is touched by human hands.

# Session 3 - [The Future Stack][future-stack] - Zack Tollman (@tollmanz), Aaron Jorbin (@aaronjorbin)

- PHP7 came out yesterday!
- Facebook pushed out HHVM, cool stuff, lets you run Hack, fast.
- PHP7 got pushed to get their shit together.
- PHP7 overhalls the internals of PHP, everything is faster, 2-3x faster.
- WordPress will warn you with depreciation notices.
- Variable variables has altered
	 - Expressions will always be processed left to right.
	 - `$$a['b'][$c]`
- List function will now go left to right, no longer accept empty variables.
- New WordPress works great with HTTP/2
	- First major HTTP upgrade in a long time.
	- It's a new web which needs a new HTTP
	- Much faster. It does this by trying to manage latency.
	- Handles latency better with multiplexing.
- Your CSS - CSS4, not around yet, but the CSS working group is starting to put together the specs that will be the future of CSS
	- `:read-`
	- `:read-only`
	- `:write`
	- `:nth-match` (not yet supported anywhere)
	- `:nth-last-` (not yet supported anywhere)
	- `color()` function, native, with no pre-compile step, in the future of CSS. No browsers yet support this.
	- Custom properties for cascading variables - native setting of CSS variables.
- HTTPS:
	- IETF - "Pervasive monitoring is an attack"
	- Some browser APIs are HTTPS only.
	- WordPress loves HTTPS.
	- Hardest is migrating HTTP to HTTPS.
	- Move to HTTPS can programmatically move people to HTTPS.
	- [Let's Encrypt][lets-encrypt] - get free certificates.
	- ACME - protocol for RESTful HTTP interface for certificate management and issuance.
	- `wp cert new` in the works.
- ECMAScript6 / Javascript2015
	- New update.
	- More modular.
	- new Promises
		- Pending
		- Resolved
		- Rejected
		- Append to promises!
		- Babel - Javascript compiler that lets you use tomorrow's javascript today.
	- Arrow functions.
		- Share the same lexical `this` as the surrounding code.
	- Javascript gets default parameters.
		- Rest parameters - all the rest of the parameters after defined defaults go into array `...a`.
	- [\#wpFutureStack][hash-search-wpfuturestack]

# Session 4 - [React + WordPress][react-wp-session] - Matías Ventura (@matias_ventura), Gregory Cornelius (@gcorne)

- "The UI helps people understand and interact with the content, but never competes with it."
- "The illusion of speed, that everything is right there immediately."
- Real time-ier.
- A declarative view layer!
- [Calypso][calypso]
	- The WP Admin as a single page application.
	- Really allows you to craft all the flows in a way that is much more smooth.
	- "waiting for a doorknob to grow before you can use the door" no more!
	- Now you have all these different states that the UI can be in. How to manage it?
	- Editor UI States?
	- Viewable all on [GitHub][calypso-github]
- React benefits
	- Small API that is easy to learn.
	- No need for a separate template language. Embrace Javascript
	- Events are bound as element properties which limits need for DOM traversal.
	- Composition of components is simple and first-class.
	- http://rauchg.com/2015/pure-ui
	- JSX
	- They compile with [Webpack][webpack] and [Babel][babel].
	- Components instead of Progressive enhancement
		- Create little packages of components, including encapsulating SASS
		- Sass goes with small components.
- Components become semantics
	- You create a syntax for your site
- Live components gallery in Calypso
- A [Boilerplate for WP plugins][wp-react-boilerplate]
- Take a look at React Native

# Session 5 - [Intent in Software Design][intent-software] - Helen Hou-Sandí (@helenhousandi)

- Naming is hard, but very very important.
- `.wp-core-ui` Javascript from core that could be front or back end.
- Be Intentional
- "Backwards compatibility is not just about accommodating the past but deliberately considering the future."
- Think about more things as very discrete components.

# Session 6 - [Build a Theme with the REST API][rest-theme-session] - Rachel Baker (@rachelbaker)

- https://speakerdeck.com/rachelbaker/build-a-theme-with-the-wp-rest-api
- Why?
	- Because you can
	- Your content needs to update or change dynamically.
	- You want to separate your business logic from your views.
- Using jQuery, Underscore.js and [Director][director-routing] for routing.
- Includes `wp_head()` to hook styles and scripts.
- Uses the `aria-live="assertive"` to tell screen readers to pay attention to what changes in the js-data window.
- Declares 3 routs. One of home, one for page, one for single posts. (All URL and permalink building occurs here)
- `site/wp-json` will list all the routes.
- Added an event handler to route visitors that click on our logo image in the header to send back to home page.
- Add logic to handle posts into its own JS file, have the homepage write that script.
- Puts the post ID on a div.
- In the API you have to keep the resources separate. Base the `&_embed` object to get a lot of the extra data and get post by post name.

# Session 7 - [REST in Action: The Live Coverage Platform at the New York Times][rest-in-action] - Scott Taylor (@wonderboymusic)

- NYT Wordpress now has a number of legacy blogs, First Draft, Internal Corporate sites, NYT Co. (Brand Site), Women of the World, Times Journeys, Live Coverage platform, and some forthcoming international projects.
- At height of blogging at NYT, 80 blogs were active. A lot used live blogging, which was a totally seperate code-base.
- NYT5
	- requires Vagrant
	- apps are git repos that require Grunt to transpile.
	- CSS compiles from SASS
	- JS compiles with Require.js
	- Used composer.
	- Had to point at NYT5 blogs app, pipe that to WordPress
	- Globals are bad.
	- Each page type is an app.
- No day archives in the NYT system.
- Use Heartbeat to pull latest posts into the side of the input area (so you can see as you blog).
	- nytimes.com/live/...
	- Backbone app that uses the REST API
	- React puts in live posts.
	- Updates are added from the backend, or via Slack which then pushes to a custom service that handles websockets.
- WordPress becomes a web service.
	- Transition to a less monolithic mindset.
	- Storage mount that is front-end via Varnish and Akami, JSON response from WP is dumped into that.
- Fire and Forget where we only post content we need.
- Custom endpoints on save_post to push out and cache data.
- Amazon SMS topic that they post to, as part of fire and forget. They send an event to the SMS queue and listening to that is a team that dynamically updates content and optimizes.

# Session 8 - [A Survey of Elasticsearch Usage][elasticsearch-session] - Greg Brown (@gregibrown)

- Search engine that is distributed and scalable.
- Analytics engine
- Multi-lingual
- Think about it as a funhouse mirror, a different way to store data.
- Pagely, VIA and WP Engine are all using with WP. As are a number of agencies, alley, and 10up.
- Six main use cases.
- Site Search
	- Better than built in search.
	- Easier to do faceted (filtered-down) searching.
	- Missing
		- Search is not just about posts
		- How to answer questions?
		- Instant results
		- Highlighted results
		- Auto complete
- Related Posts - very effective.
	- Increased click-through rate by about .5%, a big deal.
- Replace WP_Query
	- ElasticPress
	- ES_WP_Query
	- Very popular way to solve scaling problems.
- Logstash
	- Opensource
	- Imports logs and makes them searchable with ES.
	- log2logstash()
		- Dumps anything into the ES log.
	- Uses with Kibana.
- Content Reranking
	- We know this user, show them what they want, not just the general stuff.
	- ES supports lat and long to rank based on distance.
	- Show readers articles that are local to them.
- Break the blog boundary.
	- Through a ton of blogs into one big ES index to make searching and filtering easier.
	- Related posts and search over multiple sites.
- GlotPress
	- Find similar strings that have been translated.
- Additional data about images in the API.

# Session 9 - [Introduction to WordPress unit testing][unit-testing-standards] - Carl Alexander (@twigpress)

- Unit testing - at the smallest scale.
- Constant behavior, safety net.
- Isolation is the most important part.
	- Need test bubbles - surrounds your code - what is your code doing?
	- Not the same as WordPress test suites - which is integration testing.
		- Not about isolation.
- Needs
	- Unix based OS.
	- PHP5.3 for code (for namespaces), 5.4 for the tests (for traits)
	- Composer
	- WP-CLI
- WP-CLI: `wp scaffold plugin unit-tested-plugin`
- Add composer.json (package manager)
- require-dev - we need this library only when we're developing.
- require the composer autoloader
- 10up has WPMock, which is a little more limited.
- All functions must be pre-fixed with `test_`.
- Mock = test double.
	- Simulate the function or object to verify how you interact with it.
	- `expect` to get get called once with the param, if so, it returns X.
	- Works with get_option.
- Sometimes you want an array from an option.
- Write the failure case first, then make the code to not fail.
- `equalTo` vs `identicalTo` is the diff of `==` to `===`
	- "Constraint that asserts that one value is identical to another."
- Keep doing it and turn it into a habit.
- https://carlalexander.ca/introduction-wordpress-unit-testing/
- https://github.com/carlalexander/wordpress-unit-test-demo
- Unit testing makes more sense alongside biz logic.
- What you really want to test is "am I insane?"

# Session 10 - Advanced Topics in WordPress Development - Andrew Nacin (@nacin)

- "We don't want users to experience pain when they don't have to ... so we handle the edge case."
- We do break things but we figure out the most graceful, least intrusive way to do so
- We're not trying to break your plugins.
- Wrote a unit test to check to make sure that there are no ampersands in a JS file.

## Saturday

# Session 3 - [Gamify With the WordPress.com API][api-gamify] - Timmy Crawford (@timmycrawford)

- https://github.com/timmyc/doggfood
- Leaderboard for posting through the REST API.
- Can be set up to track progress.
- Can link to satisfying github issues.

# Session 4 - Lightning 1 - [I Wanna Go Fast: Advanced Techniques To Optimize Front-End Performance][go-fast] - Allen Moore (@creativeallen)

- Speed impacts user experience heavily. (Easy and pleasing to use)
- Better it deliver easily then attractively
- User engagement is important. We want users to see our content and ads.
- Keep header clean.
    - Use the async attribute on javascript.
    - Use the script loader tag to tell WP to set scripts async.
- Prioritize the critical rendering path (page speed insights helps with this)
    - Use javascript functions to load the link to your theme CSS, or to load other items asyncronously.
    - Help use javascript to load javascript to help prioritize critical tasks.
    - Use deploy script to make the css modules run.
    - CSS for above the fold should load before under the fold.
- Lazyloading.
- Prefetch, preload, prerender.
    - DNS Prefetch
        - Good for avoiding multiple hits to an external server, say to get a bunch of tweets.
        - Aquire a resource that will be used in the future.
    - Preload puts a resource in the browser cache that will be used later.
    - Prerender - downloads the assets of the DOM before it is even rendered.
- https://allenmoore.me/wordcamp-us-2015/

# Session 4 - Lightning 2 - [ARIA: Roles, States and Properties][aria-talk] - Joe Dolson (@joedolson)

- Very important to screen readers
- But a semantic meta language that can be communicated to other technologies.
- A group or properties that you can attach to an HTML object
- Roles - define what function an element serves
- States defines how you interact with an elementProperties give an element characteristics and relationships
- Can be used with CSS and JS.
- Roles can be implicit or explicit.
- `aria-level=`
    - Can be redundant, replacement, or modifier.
    - If level 1, should be h1.
- `role=`
- "What ARIA does is it enhances semantics, so it gives more meaning to content."
- "If you give [an element] that's a lie, you're actually creating confusion"
- You want to almost always avoid assigning roles that don't have matched interactions actively on the object.
- `aria-expanded="true"`
    - Is the menu open?
- Use aria attributes in styles `#menu-toggle[aria-expanded=true]`
- `aria-controls="menu-main-menu"`
    - Tells you what it is controlling.
    - Use that data to run Javascript to act on the box that the unit controls.
- `aria-label` substitutes the text of a button so that it reads something else with assistive tech
- `aria-live` critical to dynamic content, this is an area of the page that might change.
    - readers load in the DOM to allow someone to navigate it.
    - `polite` or `assertive`.
- http://www.slideshare.net/joedolson/wordcamp-us-aria-roles-states-and-properties

# Session 5 - Lightning 1 - [The Future of WordPress is Low-Tech][low-tech-wp] - Eric Mann (@ericmann)

- By cutting down their load time, YouTube was able to reach all new audiences in lower tech countries.
- Low bandwidth is really really slow (250kb/s)
- In non developed markets only 20% of devices are smartphones.
- Graceful degradation
    - turn off features and they still work.
- Progressive enhancement
    - Start for low bandwidth
- webpagetest.org
- Chrome lets you test with throttled bandwidth
- Have a device lab.
- Democratize web publishing for everyone.
- No one ever tests their sites for Windows Phones.
- "Be the change you wish to see in the world"
- Use progressive enhancement, start ad units with internal ads to fill the space properly while the JS loads.

# Session 5 - Lightning 2 - [Making use of a little known gem: The WordPress HTTP API][http-api-talk] - Ryan Duff (@ryancduff)

- cURL is lazy.
- WordPress HTTP API
- Built to work with any transport available.
- `wp_remote_*()` and `wp_safe_remote_*()`
- Need to test for WP_Error
- `wp_safe_remote_*()`
    - When user is inputing, will help avoid cross-site forgery requests.
- `wp_remote_retrieve_*()`
- [Requests For PHP][requests-for-php] by McCue
- POSTMAN or Paw for OSX
    - PAW extension by Ally Interactive generates WP API - luckymarmot.com/paw/extensions/WordPressCodeGenerator
- luckymarmot.com/paw
- http://requests.ryanmccue.info

# Session 6 - [Meeting the New York Times Challenge: delivering the news over HTTPS][news-over-https] - Paul Schreiber (@paulschreiber)

- Advertisements from web providers (like airlines) will pop in on top of HTTP pages
- A certificate can handle a single domain or multiple domains.
- Wildcard certificates let you have a single certificate for \*.yourdomain.com
- Have to show organization and domain control through validation.
- Symantec is a common certificate provider.
- So is GoDaddy.
- Resellers will get you a better deal like ssl.com
- SSL Mate
- [Let's Encrypt][lets-encrypt]
- mozilla.gihub.io/serverside-ttls/...
- github.com/tollmanz/lets-encrypt
- HTTPS enabled, HTTPS default, HSTS, submit your site to the HSTS preload list.
- SNI - SHA1 vs SHA2 - all certificates should be signed with SHA2
- Certificates are valid for a fixed amount of time. Don't forget to renew them.
- All resources will also need to be served via HTTPS.
- DoubleClick and Outbrain are the only ads now with HTTPS
- Social, font and analytics tools serve HTTPS
- Fastly charges more for HTTPS
- loadimpact.com - 1.8x faster just with HTTPS
- `content-security-policy: upgrade-insecure-requests`
- `Content-Security-Policy-Report-Only`
- `//url` is an antipattern, use `https://` instead. Except with iFrames.
- HTTPS everywhere chrome extension.

# Session 7 - [Playing well with others: writing solid code in large community projects][community-coding] - Dennis Snell (@)

- 


# Random Notes

- AeroPress for good french press coffee
- Should grind right before you make.
- Pourover method.
	- Hario makes best pourover containers.
- Crazy method - Vacuum siphon method
- March coffee festival in Brooklyn.



[techie-continuum]: https://2015.us.wordcamp.org/session/the-techie-continuum/
[dev-tools]: https://2015.us.wordcamp.org/session/the-modern-wordpress-developers-toolbox/
[vvv]: http://github.com/
[show-template-plugin]: https://wordpress.org/plugins/show-template/
[future-stack]:https://2015.us.wordcamp.org/session/the-future-stack-running-wordpress-with-tomorrows-technologies/
[react-wp-session]:https://2015.us.wordcamp.org/session/react-wordpress/
[calypso]:http://developer.wordpress.com/calypso
[calypso-github]:https://github.com/Automattic/wp-calypso
[wp-react-boilerplate]:https://github.com/gcorne/wp-react-boilerplate
[intent-software]:https://2015.us.wordcamp.org/session/intent-in-software-design/
[rest-theme-session]:https://2015.us.wordcamp.org/session/build-a-theme-with-the-rest-api/
[director-routing]:https://github.com/flatiron/director
[rest-in-action]:https://2015.us.wordcamp.org/session/rest-in-action-the-live-coverage-platform-at-the-new-york-times/
[elasticsearch-session]:https://2015.us.wordcamp.org/session/a-survey-of-elasticsearch-usage/
[unit-testing-standards]:https://2015.us.wordcamp.org/session/introduction-to-wordpress-unit-testing/
[go-fast]:https://2015.us.wordcamp.org/session/i-wanna-go-fast-advanced-techniques-to-optimize-front-end-performance/
[api-gamify]:https://2015.us.wordcamp.org/session/gamify-with-the-wordpress-com-api/
[aria-talk]:https://2015.us.wordcamp.org/session/aria-roles-states-and-properties/
[low-tech-wp]:https://2015.us.wordcamp.org/session/the-future-of-wordpress-is-low-tech/
[news-over-https]:https://2015.us.wordcamp.org/session/meeting-the-new-york-times-challenge-delivering-the-news-over-https/
