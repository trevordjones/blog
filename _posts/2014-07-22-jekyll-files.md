---
layout: post
title: "Important Files in Jekyll"
description: "Exploring other folders and files"
tags: [Jekyll, how to blog with Jekyll, Markdown]
image:

  background: lblue.png
comments: true
share: true
---

Other important files.

So I guess all of them are important, but there are a few that you will be using to get your theme to work for you, so I'm going to go over those briefly here.

##Folders first (no underline)

###assets
Most themes will have an assets folder which contains things like CSS, JS, images, and so forth. You know, important assets to your site.

###images
You guessed it - to add images to your blog, just save them in here. Use regular image files like 'jpg' or 'png'. Most themes will have an 'images' folder, though it may be buried a bit. Try looking in your 'assets' folder if you have one. You add images in different ways depending on the file you're working with. I'll be sure to go over those in later tutorials and provide you with a link to view that.

###CSS
Again, you guessed it - this is where the styling for your site goes. Or the folder may be called 'stylesheets' - it's really up to the designer of the theme since Jekyll is not picky here. I imagine all themes have this folder, though it may not be in the root directory, in which case you'll just have to dig a bit - try looking throught the 'assets' folder if you have one of those. This is completely customizable for you, so if you're a CSS guru, have at it!

There may be more in your 'assets' folder, in which case I encourage you to explore - this will help you in customizing your site. For the most part, those are the only folders in your home directory without an underline. Let's go over those folders that do have an underline.

##Underlined folders
These are some super important folders. Never change the underlined part - Jekyll uses that in the generation of your site. It's a special way of telling Jekyll to use the contents of the files inside that folder to then generate your site rather than using the files themselves. 

### _includes
Files within this folder are partials that can easily be reused elsewhere in your site, like in layouts and posts. It normally includes things like headers, footers, navigations, or quick snippets that show up often in your pages and posts - anything that can be reused throughout your site.

###_layouts
This will govern the structure of your template. It tells jekyll how to . . . well, layout your site. Since there are different pages within your site, you'll probably see a 'page.html', 'post.html', 'home.html'. So if there is a part of the actual layout of your site you want to change, maybe the home page, your best bet is to head to this folder and check out the 'home.html' (if you have one - or the file to whatever part of the site you want to change).

###_posts
Suuuper important folder and one in which you will be spending the majority of your time. You may not even touch any of the above folders, but this one you certainly will. All of your posts will be saved into this folder. So be sure to save all your posts here. I'll go more into detail on this, but the saving convention for posts is 'YEAR-MONTH-DAY-title.markup'. For instance, this post was saved as '2014-07-22-jekyll-files.md'. If you use anything other than Markdown, just be sure to include that file extension.

###_drafts
You also have the ability to save drafts on your site when they're not ready to be published. If your theme does not come with a '_drafts' folder, feel free to make one. Jekyll knows not to take any posts in this folder and make them live.

So those are the very important ones - the ones that most need your attention. The best way to learn here is to dive in and explore, but hopefully this gave you an idea of what to expect in each and how they relate to your site. Next up we'll learn about markdown and we will write our first post!