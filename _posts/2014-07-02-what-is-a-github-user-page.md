---
layout: post
title: What is a Github User Page?
description: "How to make a Github User page"
tags: [Github, User Page, Project page, Github Repositories]
image:
  feature: abstract-6.jpg
comments: true
share: true
---

## What is a Github User Page?
Good question. I couldn't figure out this very thing. Maybe I don't pick up on things as fast, or maybe I just like to know exactly what I'm dealing with and don't just take it at face value. Github explains a little bit about [pages](https://pages.github.com/) but that wasn't enough for me. Particularly I was wondering what a [User/Organization page was and what a Project page was](https://help.github.com/articles/user-organization-and-project-pages). The differences are spelled out a little, but not simply for us complete noobs.

### User/Organization Page
As a user, you are allowed one User page that Github uses to display your page. If you are part of an organization, your organization is also allowed one page. What this means is whatever you make your User page, Github will use its master to branch to show it online at 'username.github.io' (I'll explain master branches). You can check out what's on my user page at [trevordjones.github.io](http://trevordjones.github.io). This makes sense then why we can only have one (you can't have multiple sites at 'username.github.io'), so make sure it's not one of your projects or blogs. I suppose you technically could, but it's not adviseable as your address would then be 'username.github.io'. What is recommended is that you use this page as a sort of introduction to yourself. You could also include links on it to your other projects and online profiles. This makes much better sense than using it for a blog.

Github uses your master branch to display your User page. What does that mean? Each repo can have multiple branches, normally a master branch and a gh-pages branch (Github-pages branch). For a User page, Github will use the master branch to display your page online at 'username.github.io'. If you want a page for any other project (like a blog), then it would have a gh-pages branch. This gh-pages branch is the branch Github will use to display those pages you've created for your project.

Here's an example to make it a bit clearer. I have a 'introductory page' for myself at [trevordjones.github.io](http://trevordjones.github.io). This is my User page and it lives on my master branch and the repo for it is called trevordjones.github.io (trevordjones is my Github username). This is my ONLY User page. I can't have anymore. And any changes in appearance or functionality I wish to make to this page would need to be done on my master branch, because that is the branch Github is using to display the page. And it knows this because my repo is called 'trevordjones.github.io' (again, the reason this can be the ONLY User page). I also have a blog ... this blog. This blog has its own repo called ['blog'](https://github.com/trevordjones/blog). Check out the link. You'll notice there are two branches for it if you click on 'branch: gh-pages'. One is a master branch and one is the gh-pages branch. The original template I used for this blog lives on my master branch. This is the *original*. When customizing my blog, I do not make any changes to this branch. Why? Github isn't using this page to display my project - so why make changes? Plus it's nice to know what the original was in case you make a mistake and need to start over. This blog is using a gh-pages branch. So try clicking on the master branch and you'll notice there are fewer files in there as well as changes to the files from my gh-pages branch. My gh-pages branch is what Github is using to display my blog (with the use of Jekyll). This is a *Project page* and I can have as many as I want. I can even give them custom domains, again, like I did with this blog.

As a side note, you can also visit this very same blog at [trevordjones.github.io/blog](http://trevordjones.github.io/blog/). See how my blog (gh-pages) is *branching* off my master (trevordjones.github.io)?? Moving on now. 

What I will teach you below is how to set up your User page (which can also be used if you're setting up an Organization page). Here is the tutorial for setting up a [Project page]({{ site:url }}/what-is-a-github-project-page), which is very similar. Also feel free to see Github's tutorial at [https://pages.github.com/](https://pages.github.com/). (I will dig into that tutorial more for the project pages tutorial)

#### How to set up a User/Organization Page
Now that you (hopefully) understand pages, on to the good stuff. Make a [repository](https://help.github.com/articles/create-a-repo) (or repo) and name it 'username.github.io' (please use your username here ...) Your full repo should then read 'username/username.github.io'. Then whatever you make here will live at 'http://username.github.io'. It's adviseable that you make this a sort of introductory page for yourself as mine is. Again, you don't want a full blown project living here. You can put links on here for those projects/websites. This is great for an organization as well if you want to show off links to what your team is doing on a nice, customizable page. These steps below are for a User page, but an Organization page has the very same steps - you just do it through your organization rather than through your own account. And I'll be using the terminal for Mac, so substitute Command Prompt for Windows.

If you don't want to use one of Githubs themes for User pages, you don't need to. This just requires that you create your own theme for the look of your page. If this is the case, you only need to do 4 steps (after creating your theme of course, which may take time - and this is not an html/css tutorial, so hopefully you already know how to do that. If not, use the theme). The steps:

1. Create your repo in Github and name it 'username.github.io' - you MUST use this naming convention - it's what tells Github that this is your User page.
2. Next you'll see a page that looks like the image below. Copy the link under the 'Quick Setup' section. It should look like 'https://github.com/username/userpagename.git' - your repo is now created! 
pic
3. Go to your terminal, be sure you're in the folder that holds your theme (I recommend calling your folder the same name as your Github repo), then enter the command: `git remote add origin` and past the url you copied in step 2. Hit enter.
4. Now push your folder to github so the theme can be applied to your User page (If you're unfamiliar with Git and Github, check out my [Git tutorial](http://www.trevordjones.com/git):
* `git add .` (the period is supposed to be there - use it to add all the files to Git)
* `git commit -m "type your message here"
* `git push origin master`

Any changes you make at a later time can be added to Github using step 4. Work on it locally on your computer, then push it to Github. That's all.

For those who want to use a Github theme (don't worry, you can also customize easily with html and css) just follow these steps:

1. Create your repo and name it 'username.github.io' - you MUST use this naming convention - it's what tells Github that this is your User page.
2. Click the 'Settings' section along the right hand side.
3. Scroll a little ways down and you'll see a 'Github Pages' section.
![Create repository]({{ site:url }}/images/create-repository.png)
4. Click 'Automatic page generator'.
5. Name your project, then skip to the bottom and click 'Continue to layouts'.
6. Pick out a theme. Take your time, find one you like.
7. Publish it.
8. Wait for a few minutes, then in your browser go to 'username.github.io'.

Follow these instructions and you shouldn't get lost. If you don't see your site, wait a couple more minutes and refresh again.

If you want to work on this locally (through a folder on your computer) and not on Github, then you can follow these steps using Git. I actually recommend working locally as it gives you a chance to test it out before it goes live on Github. So to continue:

9. Clone your User page to a folder on your computer. Along the right below 'Settings' you'll see a link you can click on called 'clone url'. Just click to highlight, then copy.
10. In your terminal navigate to where you want this project to live. Type in `git clone` (and paste the url you copied).
11. Now if you go to the folder you cloned the project to, you'll see a new folder called 'username.github.io'. Click into it and you'll see all the files/folders of your User page.
12. Feel free to customize anything. If you used one of the theme options, you should have all the files of a normal website, including an index.html file and folders for images, stylesheets and javascript. Customize this however you like. Don't worry about the README, favicon,  params or .DS_store files.
13. Once you've put all the finishing touches on it, `push` it back to Github. To do that, go to your terminal, make sure you're in the correct folder then:
* `git add .` (the period is supposed to be there - use it to add all the files to Git)
* `git commit -m "type your message here"
* `git push origin master`

Then refresh the page for `username.github.io` and you should see your changes take effect! If you got lost for step number 9, please check out my [Git tutorial](http://www.trevordjones.com/git). That's it for User pages. If you create one from this tutorial, feel free to put a link to it below in the comments section!