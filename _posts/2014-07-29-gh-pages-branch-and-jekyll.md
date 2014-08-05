---
layout: post
title: "Publishing Jekyll Blog with gh-pages"
description: "Publish your blog with the gh-pages branch"
tags: [Jekyll, how to blog with Jekyll, gh-pages]
image:
  feature: abstract-5.jpg
comments: true
share: true
---

Let's make a gh-pages branch.

If you haven't already or if your blog did not come this way, you're going to want to create a gh-pages branch. Mine for instance came with both a master branch and a gh-pages branch when I forked it. If you downloaded first and then pushed it to Github, then you should have a master branch only.

Of course, if you want your blog to be your User page, then you'll want your blog to live on your master branch and you won't have to worry about the gh-pages branch. If you're unsure of what I'm talking about, view my Github [user page]({% post_url 2014-07-02-what-is-a-github-user-page %}) post and [project page]({% post_url 2014-07-04-what-is-a-github-project-page %}) post.

So, if it came with both a master and a gh-pages branch, you'll want to delete the gh-pages branch as I'm sure it has a ton of their own content and customizations that you don't want in your own site. You can delete in Github by clicking on the 'branches' link along the header of your repo:

![Github branch link](/images/github-branch-link.png)

You'll have to make sure the gh-pages branch isn't your default branch. If it is, you'll have to change it in your 'Settings' along the right hand side of your main repo page. 

![Github default branch](/images/github-default-branch.png)

##WARNING
Do NOT delete your gh-pages branch if you have no master branch. If this is the case, then simply create a master branch (so in a way you can have an 'original'). Now just ensure that gh-pages is your default branch. Now any customizations you make should be pushed through to your gh-pages branch.

###If you downloaded your theme to your computer
When you initially push it to Github it will come with a master branch. Make a repo in Github (the same name as your folder) and follow the instructions to push it to Github. 

###Terminal
In your terminal you should also have two branches. Navigate to where your blog lives and in your terminal type:

	git branch

to see a list of branches. If you don't have a gh-pages or master branch, type:

	git checkout -b gh-pages
	
Or `master` if you need a master branch. You can switch back and forth between branches by typing:

	git checkout 'branch-name'
	
If you created a branch here, you need to push that to Github. Make sure you're in the correct branch and type

	git push origin 'branch-name' 

From here on out, let's use the gh-pages branch, as that is the branch Jekyll will be using to publish your site. All of our changes to the blog and pushes to Github will be through this branch. 

###If you created a gh-pages branch on Github and not your terminal
You're going to want to pull it to your terminal. First make a gh-pages branch in your terminal

	git checkout -b gh-pages

And then

	git pull origin gh-pages

Now just ensure that locally you always work on this branch, and whenever you make a change and want to push it back to Github, use:

	git push origin gh-pages
	
(after you add and commit of course).

If anything was confusing, comment below. But remember that `git branch` is your friend. Use it to find out which branch you're on and if you have the right branches. Use `git checkout` if you don't.

Let's check out the site. First, make sure the config file in your gh-pages branch has the appropriate url (or baseurl depending on the theme). For now (until you publish with your own domain) you'll want this to be http://username.github.io/repo-name. Substitute 'username' and 'repo-name' appropriately.

Once that is done, you can visit username.github.io/repo-name and see your blog! Changes sometimes take a few minutes to take affect, so if you don't see it right away, trying again in a minute or two. Leave a comment with a link if it didn't work.
