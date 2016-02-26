---
layout: post
title: "Rails: Include a Single JS File in View"
description: "Including a single JS file in your view"
tags: [Rails, JavaScript, Asset Pipeline]
image:
  feature: abstract-5.jpg
comments: true
share: true
---

Something that drove me crazy was figuring out how to include a JavaScript file in a single view. Maybe it's a lot of code you don't want to run on every single  page load. The Rails pipeline is great but makes this task difficult. Maybe I was looking in the wrong places but it took a while to find a solid solution.

This is NOT an asset pipeline tutorial, so I won't go in depth with that. However, you do need to know that all your JS files will be included in each view because of the `//= require_tree .` inside of the `application.js` file. If you keep this, then you will not be able to include a JS file in a single view, obviously. So remove that line.

But what if you have lots of files that need to be used across many views and this is the best way for you to do it? No problem - organize the files into appropriate directories and then include those directories in the `application.js` file. If you have a `factories` directory, then it would be `//= require_tree ./factories`. If your code is organized well, you shouldn't have to require too many items. Writing a few more lines is a good sacrifice if it means your app doesn't need to load large JS file on every page load.

Next you need to make sure this file can be precompiled. Requiring the `application.js` file normally takes care of this for you, so you've never worried about it before. But now you need to. Head over to the `config/initializers/assets.rb` file and look at the line

	Rails.application.config.assets.precompile += %w()
	
You'll need to include the file in here, so it looks like:

	Rails.application.config.assets.precompile += %w(example.js)
	
If it's in a directory, then it will look like:

	Rails.application.config.assets.precompile += %w(directory/example.js)
	
If you don't know what `%w` does, I recommend you fire up an `irb` and run it to find out. 

	%w(what the heck does this do?)
	
Next, restart the server. Most anytime you deal with things in the config directory (especially the initializers), you need to restart the server.

Then in the view where you want to include your JS file, just use `javascript_include_tag` and list the file name in quotes!

	<%= javascript_include_tag 'example' %>
	
If you look at `application.html.erb` you'll see that Rails does the same thing - they just include the `application` file, which as you know requires any other files listed within it. 

It's not hard, but this can sure come in handy!