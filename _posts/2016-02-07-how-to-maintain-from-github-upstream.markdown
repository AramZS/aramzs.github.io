---
title: Maintaining an abandoned project from upstream on GitHub
date: 2016-02-07 19:34:51 Z
categories:
- open-source
- GitHub
layout: post
vertical: Code
excerpt: How to deal with an abandoned project without leaving the tree.
---

Sometimes you're working with an open-source code library that has a number of interested contributors but has been abandoned by the project maintainer. There are a few options for keeping the project up to date. The most obvious one is to cut the branch off the tree and start your own repository. However, that's not always the optimal solution. Sometimes the maintainer is fairly high profile, or the code is linked in a lot of places, or for whatever reason abandoning the base git tree just won't work.

In that case, there are options for essentially running the project from upstream; where you keep your branch attached to the original project tree, but pull in the pull requests from other interested parties. Using this technique you can keep your branch up to date with the best pull requests, but without fracturing the project. In addition, if the project maintainer ever comes back, they'll have a handy single pull request with all the new features that you've been maintaining.

This is based on [a StackOverflow response][stackoverflow].

First you'll want to add the other upstream fork as a remote of your repository.

{% highlight bash %}
{%raw%}

git remote add otherfork git://github.com/request-author/project.git

{%endraw%}
{% endhighlight %}

`otherfork` in this example is the name you are giving the remote repository (like origin). You can add as many other forks as you'd like, as long as you give them different names.

If you find that the other upstream repository is storing their commits for the pull request on something other than their `master` branch, then you'll need to bring those other branches in too.

`git fetch otherfork patch-branch`

Once that is done, you can treat `otherfork/patch-branch` like any other  branch in your repository. If you want to bring in the commits from the pull-request on the downstream project, you have a few options.

You can `cherry-pick` the SHA of the commits you want to integrate:

`git cherry-pick <first-SHA1> <second-SHA1> <etc.>`

You can use a standard merge, or a `git pull`:

`git merge otherfork/patch-branch`

or

`git pull otherfork patch-branch`

Using these methods you can have your version of the codebase living upstream of the project base but still examine, test and merge pull requests to the base as if you were the project maintainer. This should make it easier to have up-to-date code without fragmenting the project.

[stackoverflow]:http://stackoverflow.com/questions/6022302/how-to-apply-unmerged-upstream-pull-requests-from-other-forks-into-my-fork
