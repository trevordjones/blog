---
layout: post
title: "How to Set up Your Jekyll Theme"
description: "Set up a Jekyll theme"
tags: [Jekyll, how to blog with Jekyll, Markdown]
image:
  feature: abstract-3.jpg
comments: true
share: true
---

## Setting up your Jekyll Theme

Alright, there are two ways to do this:

1. Fork it from the designer's github and then clone it to your computer
2. Download to file directly to your computer, make a repo in Github, then push it to Github

### Clone the theme

If you followed my [last post]({{ site:url }}/use-a-jekyll-theme) then you should have a repo in your account with all the folders/files for the theme. Let's clone this to your computer. Go to that repo and in the bottom right corner you'll see a 'HTTPS Clone URL' section with the url below it. Click on it and it should all be highlighted. 

Open up your [terminal]({{ site:url }}/terminal) and navigate to where you want your blog to live, like in a 'projects' folder. Once you are there, run the command `git clone` and past the url. Now it should be on your computer!

Now you can open it up in your text editor of choice. Look around at all the files and try to get familiar with it's layout. I'll dive into this deeper but important files to know about are the _config.yml, index.html, and all the folders at the top. Those do some heavy lifting with your theme.

### Download the theme
 
The other way to get it on your computer is by downloading it. Each theme you visit from jekylltheme.org will have a download link. Also, you may have purchased a theme, which will also give you a link to download it. Stick the theme in a folder on your computer and let's push it to Github.

Go to your Github account and [create a repo](https://help.github.com/articles/create-a-repo). Once you've done that you'll see instructions on what to do with Git. You will want to 'Push an existing repository from the command line'. Copy that first line: `git remote add origin https://'github-url'` and paste it in your terminal and run it. MAKE sure you are still in your blog folder!! If you click on this folder it should open up all the files and folders in your blog theme. You MUST be in that folder.

Next copy the following command `git push -u origin master` and paste it to your terminal and run it. There! If you look at your repo on Github you should see all the files/folders of your theme.

#### All done with that part
Ok, you are ready to forge ahead. Next we're going to learn about many of the files in your newly created blog! Let's hit up the [config file](/jekyll-config-file) first.