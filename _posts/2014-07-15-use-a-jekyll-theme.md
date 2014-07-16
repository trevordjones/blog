---
layout: post
title: "Use a Jekyll Theme"
description: "Find and use a Jekyll Theme"
tags: [Jekyll, how to blog with Jekyll, Markdown]
image:
  feature: abstract-4.jpg
comments: true
share: true
---


## Use a Jekyll Theme
To get you initially set up and running with your blog, you're going to want to use a theme. As you get more comfortable with Jekyll you can really tweak the theme to make it your own or even create your own theme! Which would be awesome. For now, we'll use someone else's. It has all the files/folders necessary for Jekyll so it makes it really easy (and then it's easy to customize as you'll have full acess to all the files).

There are free themes at [jekyllthemes.org](http://jekyllthemes.org/) and you can surely find premium themes at [Theme Forest](http://themeforest.net/search?utf8=%E2%9C%93&term=jekyll) or another site like that. For our tutorial, we're going to use jekyllthemes.org because we'll be forking it from the designer. 

So head over to that site and pick your favorite theme!

There are a few ways to get the theme on your computer. Let's clone it from Github first. If you don't want to do that, skip over to my cloning/downloading instructions.

If you're completely new to Github, then please review my [Github tutorial]({{ site:url }}/github). Cloning it from Github:

* Click on the theme and then click 'Home'- some of the themes will take you to their Github account. Some will not.
* For those that don't, search on google with keywords like 'theme name' + 'github' + 'author name'. You should be able to find a github link and then you can find their repo.
* If all else fails and you can't find one (I couldn't find the repo for Vanilla Bean Creme) then you'll have to download it and skip to my [next post]({{ site:url }}/set-up-jekyll-theme).

You should now be in this person's Github repo for their theme - it should look something like this:

![Designer's Github]({{ site:url }}/images/github-jekyll-theme.png)

In the upper right corner click on the 'Fork' button and fork it over to your account. Now you should have a repo like `github.com/username/theme-name`.

Let's edit it. Along the right you'll see a 'settings' option - click that and it will bring you to a place where you can change the name of the repo. I changed mine to 'blog' - I feel it's descriptive enough, but make it anything you like. Click 'Rename' and head back to your repo.

Now on the line right underneath the repo name, you'll see a section you can edit:

![Edit Repo]({{ site:url }}/images/edit-repo.png)

Go ahead and make changes here. For now, make the website `username.github.io/'repo-name'`. You won't find it at that url yet, but you will. If you want to look at an example, mine is [github.com/trevordjones/blog](https://github.com/trevordjones/blog). You can take a look to see what I did.

Ok, now you have the theme set up on your Github account. It has all the files Jekyll will need to parse your blog and display it properly. Now it's time to make it yours by [cloning it]({{ site:url }}/set-up-jekyll-theme) to your computer!