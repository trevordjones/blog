---
layout: post
title: What is a Github Project Page?
description: "How to make Github Project pages"
tags: [Github, User Page, Project page, Github Repositories]
image:
  feature: abstract-7.jpg
comments: true
share: true
---

## What is a Github Project page
This is a continuation of [Github User Pages]({{ site:url }}/what-is-a-github-user-page). If you don't recall (or want to know) what a User page is, read that link. Project pages (or sites) are for displaying your projects. Basically, you're able to display it outside the confines of Github - meaning you can make it look snazzy and can give it a url of 'username.github.io/project-name'. Of course, you don't have to display your project if you don't want it to have it's own site. If displaying it through your repo on Github is all you want, then great! 

Let me show you what I mean to help clarify. This is my blog - it's considered a Project page. I already have a [User page](http://trevordjones.github.io). I also have a [repo for my blog](https://github.com/trevordjones/blog). But I don't want readers to have to dig through this repo in order to find my posts - what kind of user-friendly blog is that!? No, I want to display it on a Project page.

### How to set up a Project page
If you did the User page tutorial, you'll find that making a Project page is very similar. I'm actually just going to reference the [Github Pages](https://pages.github.com/) site as it's a little more helpful than the User page tutorial, though I will explain it more. It really is fine if you follow their instructions to the T. But what I found difficult was the fact that I didn't know what I was doing. Sure I can follow instructions. But what am I doing this for?? So finish reading the post, get an understanding, then follow their tutorial.

If you read my first two paragraphs, you should have a better idea of what Project pages are and why you would (or would not) create one. Are you making a blog? Then definitely use a Project page. Are you writing a ruby gem? Then you probably don't need one. The scope of your project will help you decide if you should or should not have one. Generally speaking, if it needs a custom domain, then you definitely need a page. If you can explain it well in the README, you don't need one (though you could). 

Project pages are also built on gh-pages (or github-pages). This is just a branch from your master branch and this branch will be used for displaying your project. This means you can work on any change that is needed for displaying your project (because these changes should be made in the gh-pages branch) without actually changing your project in the master branch. Feel free to check out my [blog repo](https://github.com/trevordjones/blog) and look through both my master branch and my gh-pages branch. You'll notice that there are differences - the master branch is holding the *original* template.

So go ahead and follow the [Github Pages tutorial](https://pages.github.com/). For a Project page, click on 'Project site', then 'Generate a site'. When you get to step 3, come back here.

### Adding content
Github can use a markup language called Markdown (yes, very funny). It has similarities to HTML but it's meant for *writing*, not for helping to create an actual site like HTML. You can use it on a project page for writing the README, writing [blog posts](https://github.com/trevordjones/blog/blob/gh-pages/_posts/2014-06-23-github.md) (I'm using Markdown), or writing any kind of content in your site. I mention this just because the picture in the tutorial is using Markdown, and you'll see it throughout other people's Github repos. I was super confused by this and I don't want you to be. To learn about how to use Markdown, check out this [cheat sheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet). Reference the cheat sheet and feel free to write some content like the tutorial suggests. Then proceed to step 4.

Once you're done with the tutorial, do as it says and go to your site. It will be 'username.github.io/repo-name'. This blog for instance can also be found at trevordjones.github.io/blog. See your site? Cool! From here, you can do just about anything with your site. You can clone it to your computer (if you haven't already), make changes to it locally in a folder on your computer, and push those changes up to Github. If you have no idea what I'm talking about, then check out my [Git]({{ site:url }}/git) and [Github]({{ site:url }}/github) tutorials. Just be sure that when you push your changes to Github, you use `git push origin gh-pages` because remember, you project will be displayed through the gh-pages branch of your repo. 

That's all for Project pages - ask any questions below if something doesn't make sense.









