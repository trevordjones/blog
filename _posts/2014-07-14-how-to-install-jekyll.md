---
layout: post
title: How do you install Jekyll?
description: "Figuring out Jekyll"
tags: [Jekyll, how to blog with Jekyll, Markdown]
image:
  feature: abstract-11.jpg
comments: true
share: true
---

Here are some pre-requisites for getting Jekyll installed. 

After this, you'll probably see why Jekyll says it should only take a few minutes to install, because for the already initiated programmer, they should already have/know all this stuff. But for those who don't...

Here are your pre-recs:

* Mac, Unix or Linux operating system. Sorry Windows users - it's possible for you to use but more complex and extra setup. View [Julian Thilo's tutorial](http://jekyll-windows.juthilo.com/) - it's a great tutorial and easy to follow.
* You'll need:
	* Ruby
	* RubyGems
	* NodeJS
	
The [Jekyll documentation](http://jekyllrb.com/docs/installation/) has some good links if you're not sure how to get those installed. If you're not sure if you already have them, go to your terminal.

If you're unfamiliar with the terminal, then check out my [terminal tutorial]({{ site:url }}/terminal). You'll probably also want to check out the [Git]({{ site:url }}/git) and [Github]({{ site:url }}/github) tutorials, as we'll be using those later, but just look at the terminal tutorial for now.

If you are familiar with terminal (or have become familiar) we can check that we have these installed. Open the terminal and type in `ruby --version`. To check on RubyGems, you can `gem update --system`. If you have RubyGems, it will be updated, if not, then you'll know you don't have it and need to [download it](http://rubygems.org/pages/download). For NodeJS - type in `node` in your terminal. If it's not [installed](http://nodejs.org/), you'll probably get an error, if it is, you'll get a new line with a `>` at the beginning of it. 

Once you have all that setup *and* are familiar with the terminal, you can get all set up. In the terminal run `gem install jekyll`. If you run into problems, the Jekyll documentation is helpful - you most likely need to install (or update) Xcode (for a Mac). You can get it/update it from your app store.

That's it! If you're looking at Jekyll you'll see a bunch of other stuff about installing different versions. As you're most likely a beginner with Jekyll, that all is irrelevant, so don't worry about it. 

