---
layout: post
title: "Jekyll Config File"
description: "Configuring your config"
tags: [Jekyll, how to blog with Jekyll, Markdown]
image:
  feature: abstract-8.jpg
comments: true
share: true
---

By now you should have your theme set up in your blog repo on Github. Now it's time to dive into the themes to prep them for displaying online! 

First we'll tackle the _config.yml file. There are tons of cool stuff in here you can edit to customize your site. Go ahead and open it up.

This file is called 'config' because it really does configure your site. See all the text in read (I guess depending on your text editor . . . )? But see it along the left? Leave that alone. The stuff on the right you can then customize. Every Jekyll theme has this set up differently, so you're more or less confined here to what they have added. As you dig more into Jekyll you can probably figure out ways to add more - if you check out mine, my theme has a lot of customizations I can configure. 

But you can't just add:
	
	reading_time:
	url:
	email:
	twitter:
	
to your config and then hope it works. It all depends on how those items are called in other files, which you won't know until you dig more into them (some might not even use them). So you can at some point - but I'm assuming you're a beginner, so let's not for now.

So if your config file doesn't allow you to include your social links, google analytics and so forth, you can certainly switch up themes and try another one. Next time, view the config file before downloading or cloning.

But this really is as simple as that - no need for hard coding here. Just put in what it's asks. For things like your social network, just at the user name - anything after the '.com' - so for twitter, it would be your user name. Same goes for Facebook, though it might take some experimenting with to get the proper syntax per how their theme interacts with the config file.

And if there's something you don't want to include, it's perfectly fine to leave blank. I figured mine out simply by following the designers instructions (he left comments - super nice. Again, switch up themes if yours isn't user-friendly) and by trial and error. I made some changes, then viewed my website to see where those changes took effect. For instance, mine has a 'links' section - I looked at the links that were already included and then went to his blog to see where they appeared. I copied how he did and just included my own and took out his. 

Like I said, as you get more proficient with Jekyll and their templating language, you can start to add your own fields and create your own templates. Feel free to have a look through their [config documention](http://jekyllrb.com/docs/configuration/) though it's super confusing unless you already know what they're talking about. But no harm in reading through it.

That's all for now!