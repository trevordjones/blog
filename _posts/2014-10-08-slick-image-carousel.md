---
layout: post
title: "Setting up Slick Image Carousel"
description: "Getting your Jekyll blog live with your own domain"
tags: [Image Carousel, Slick, JavaScript]
image:
  background: bg3.png
comments: true
share: true
---
How to set up the Slick Carousel

Slick is just that- slick. It's an awesome way to include an image slider/carousel in your website without adding heavy code to your site. What makes it so great is it's easily customizable. You have full access to the CSS and JavaScript files and Ken Wheeler added a few things to make is plain easy. Only problem is, there are a couple things missing from the documentation and it can be hard to set up initially. This will walk you through getting it set up from a blank website.

First thing to do is to [download Slick](http://kenwheeler.github.io/slick/) (and come back here). If you already have a website up and going, then you can just copy over the files. You can also use the CDN so you wouldn't have to download but I don't recommend it as it's more confusing and you have no customization ability. Stick with downloading it into your app.

The next thing you want to get is your images lined up. I'm just going to use the default images he provides of Fonzie but put up whatever ones your were planning on working with.

This next step is the one that's not so greatly documented: Linking the necessary files to our view page. Starting out with CSS, link the `style.css` and the `slick.css` files that come with the download. Your head should then look something like this:

{% highlight html linenos %}
<head>
    <meta charset="UTF-8">
    <title>Slick Carousel</title>
    <link rel="stylesheet" type="text/css" href="css/style.css">
    <link rel="stylesheet" type="text/css" href="slick/slick.css">
</head>
{% endhighlight %}

I believe the documentation only tells you about `slick.css` but `style.css` is just as crucial. I know, frustrating.

Next we'll attach our scripts. You're going to want jQuery first, then two scripts that come with Slick: `scripts.js` and `slick.js`. For this tutorial, I'm going to use the CDN hosted jQuery, but use whatever you're comfortable with. Be sure to put the jQuery script first as the other two rely on it. Your file should now look like:

{% highlight html linenos %}
<body>
    <script type="text/javascript" src="http://code.jquery.com/jquery-1.11.0.min.js"></script>
    <script type="text/javascript" src="js/scripts.js"></script>
    <script type="text/javascript" src="slick/slick.js"></script>
</body>
{% endhighlight %}

Next we'll put in the images. Create a div and give it a class `single-item`. Within that div, put in all your images. Make sure each image has it's own div. It should look like this:

{% highlight html linenos %}

div class="single-item">
    <div><img src="img/lazyfonz1.png" alt=""></div>
    <div><img src="img/lazyfonz2.png" alt=""></div>
    <div><img src="img/lazyfonz3.png" alt=""></div>
    <div><img src="img/lazyfonz4.png" alt=""></div>
    <div><img src="img/lazyfonz5.png" alt=""></div>
    <div><img src="img/lazyfonz6.png" alt=""></div>
</div>

{% endhighlight %}

If you refresh your page now you should have a big image covering the entire screen. Below it you'll see the dots which you can click on to move back and forth between the images. This looks great! Ok, maybe not. Maybe you don't want to fill the entire screen with a single image. Go to your `style.css` folder and do

{% highlight html linenos %}
single-item {
    width: 40%;
}
{% endhighlight %}

There, that should look better. If your screen has a background of white you may think there are no arrows. But they're there. They are white as well. You can change the positions of the arrows by going into `slick.css` and finding the arrows section. For the classes `slick-prev` and `slick-next` change the left and right from -25px to 25px. Refresh and there they are! You can position these wherever you want.

How is this all working? We gave the the wrapper div a class name of `single-item` and we can see the specifications for this class in the `scripts.js` file. We can actually see all the options we have for class names in here and can tweak them as we wish. Click "Settings" on [Slick's site](http://kenwheeler.github.io/slick/) to see what all your options are for tweaking each class. The options as you can see are listed out as a regular JavaScript object. If you're unfamiliar with this, just try to copy what's in there exactly if you're adding new settings. Play around with the different classes and settings to see what all you can do with your Slick carousel! 

As you can see, this is an amazing image carousel/slider. And once you know about the missing CSS and JavaScript files in the documentation, it's a breeze to install and has amazing customization. You can include any kind of arrows you want, and have a wide range of options for the appearance of your carousel.