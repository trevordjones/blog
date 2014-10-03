---
layout: post
title: "AngularJS and Slick Image Carousel"
description: "Getting your Jekyll blog live with your own domain"
tags: [AngularJS, Image Carousel, Slick]
image:
  feature: bg2.jpg
comments: true
share: true
---

Create an image carousel with AngularJS and Slick!

This post will utilize Slick's AngularJS version of their sliding image carousel. This is also geared towards those who are still trying to learn AngularJS and JavaScript (or those who got lost with the documentation). If you look through the [Github repo and README](https://github.com/vasyabigi/angular-slick) you'll notice there is some lack of documentation. This post will help walk you step by step to getting your own carousel up and running. However, I do assume that you have some knowledge of AngularJS.

There are several AngularJS carousel's you could apply this to but I like Ken Wheeler's Slick the most and I think it's the most 'editable' of any of them, so it's my personal choice. But let's get started.

First create an empty folder in which your carousel application will live. Get in to this directory and run `bower install angular-slick`. While you're still in the terminal, run `touch index.html`.

The documentation for the next step is actually much more helpful than other AngularJS image sliders. Copy 

	<link rel="stylesheet" href="bower_components/slick-carousel/slick/slick.css">
	
into the head portion of your index.html file. Then in the body, copy
	
	<script src="bower_components/jquery/jquery.js"></script>
	<script src="bower_components/angular/angular.js"></script>
	<script src="bower_components/slick-carousel/slick/slick.js"></script>
	<script src="bower_components/angular-slick/dist/slick.js"></script>
	
right before the end of your body tag. Your carousel app should now have AngularJS (the documentation has a slight error here, but more on that further down). In the html or body tags, include `ng-app` and your final product will look like:

{% highlight html linenos %}
<!DOCTYPE html>
<html lang="en" ng-app>
<head>
	<meta charset="UTF-8">
	<title>Slider Practice</title>
	<link rel="stylesheet" href="bower_components/slick-carousel/slick/slick.css">
</head>
<body>
	<script src="bower_components/jquery/jquery.js"></script>
	<script src="bower_components/angular/angular.js"></script>
	<script src="bower_components/slick-carousel/slick/slick.js"></script>
	<script src="bower_components/angular-slick/dist/slick.js"></script>
</body>
</html>
{% endhighlight %}

This next step is where it gets confusing for those who are new. You're supposed to add the dependency module `slick` to the app. So . . . haha, what do you do?

1. Create a new folder (outside of the bower_components folder) - call it 'js' or whatever you call the folder which holds your JavaScript files.
2. create a new file - 'app.js' or whatever you want to call it. Within this file, include:
	
		'use strict';
		angular.module("app", ['slick']);
	
3. Inside your index.html file, set ng-app to the name of your app:

		'<html lang="en" ng-app="app">
		
4. Add this file below the last script inside your body elements.

		'script src="js/app.js" 
		
Ok! That step is done. Next, let's include the `slick` element in our html. If you're not sure what we're doing here, read up on [AngularJS directives](https://docs.angularjs.org/guide/directive). The Slick AngularJS we downloaded comes with a built-in directive allowing us to use it as an element here in our HTML. So now you'll have 

	<slick>
	
	</slick>
	
And this is as far as the documentation takes you, which is a little upsetting. Let's finish up by putting some images in here. If you haven't already, get your pictures ready and store them in an 'images' folder. Then add them to your html - be sure to separate out each image with its own div, like so:

{% highlight html linenos %}
<!DOCTYPE html>
<html lang="en" ng-app>
<head>
	<meta charset="UTF-8">
	<title>Slider Practice</title>
	<link rel="stylesheet" href="bower_components/slick-carousel/slick/slick.css">
</head>
<body>
	<slick>
	  <div>
	    <img src="img/photo_1.jpg" alt="">
	  </div>
	</slick>
	<script src="bower_components/jquery/jquery.js"></script>
	<script src="bower_components/angular/angular.js"></script>
	<script src="bower_components/slick-carousel/slick/slick.js"></script>
	<script src="bower_components/angular-slick/dist/slick.js"></script>
</body>
</html>
{% endhighlight %}

Have all your photos listed out like that (be sure to have 4+ photos at least). So now, one would expect to be able to open this page in the browser and find an image slider. But not so! You just see your images going down the page, which makes it look like the `slick` element isn't working at all. And this is the glaring hole in their documentation. There is one more css file we need to include. Copy and paste this in your head section:

	<link rel="stylesheet" type="text/css" href="bower_components/slick-carousel/css/style.css">
	
This is an incredibly important bit of css that will finish off the styling of your slider and allow you to customize as you like. Why it's left out is anyone's guess. Now let's refresh the page - wait, it still doesn't work! Gotcha again. If you open up the console you'll see there was an error fetching your JQuery file. Well, turns out they give you the wrong location for it. Go back to your body and where the script element is for JQuery, substitute it with this:

	<script src="bower_components/jquery/dist/jquery.js"></script>
	
I guess they forgot the 'jquery.js' file is located in the 'dist' folder. I don't know. Now refresh your page. You'll most likely get a big image of your first picture with no way of sliding over to the next one. We're on the right track.

We want to add some additional settings to our 'slick' element to allow us to scroll through the images. If you're unfamiliar with Slick, this is the part that is amazing and why I like it so much. It's dead simple to get your slider to look/act the way you want. You have tons of options to include. Click to go to all [Slick settings](http://kenwheeler.github.io/slick/#settings). Anything you want to add, you do so like this: 

	<slick dots=true infinite=true speed=300 slides-to-show=3 slides-to-scroll=3> 
	
This will add the dots to the bottom of your carousel, change images at 300 milliseconds, show 3 images at once, and scroll 3 at a time. I encourage you to look through the list and add things to see the result.

Now when you refresh the page you should see 3 images and some dots at the bottom. In my case, I don't see arrows on either end of my images, so I have to click on the dots to scroll back and forth. So if you can't see arrows either, lets get those added.

Head over to the style sheet by going to 'bower_components/slick-carousel/slick/slick.css'. You'll see a commented out line that says "Arrows". You'll want to change the positioning for 'slick-prev' and 'slick-next'. You'll see that 'slick-prev' has a left of -25px and 'slick-next' has a right of -25px. Just remove the negative signs. Refresh the page and you should now see them!

Obviously there's a lot more you can do here. If you wanted to clean up your html you could use 'ng-repeat' and store the images as an object in a controller. You can customize the styling, change up how the arrows look and so on. Have at it! Leave comments below if you couldn't get it set up.

 