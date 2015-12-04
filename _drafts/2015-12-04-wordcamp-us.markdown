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
