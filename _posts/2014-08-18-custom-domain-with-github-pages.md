---
layout: post
title: "Custom Domain with Github Pages"
description: "Getting your Jekyll blog live with your own domain"
tags: [Jekyll, how to blog with Jekyll, Github Pages]
image:
  background: bg2.jpg
comments: true
share: true
---
Last step - setting up your custom domain for Jekyll.

This last part can be a little confusing but it's actually more confusing with the service you registered your domain with. But here's a quick rundown:

###Custom Domain with Github Pages

Remember that your site is hosted on Github, not Jekyll, so this will actually require working more with Github Pages than Jekyll. I'm sure you've come across their instructions, but if not, [here is a link](https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages). Here I've consolidated it all as theirs goes across a few pages.

####Adding a CNAME
It's as easy as it sounds. In your text editor, create a file called `CNAME` - no file extension, just all upper case `CNAME`. In this file write your domain. I just wrote 'www.trevordjones.com'. Then add and commit, then push it to Github (gh-pages of course). Ok, that's all you need to do on this end.

####Setting up your DNS provider
This will be a little different depending on your provider, but I'll try to guide you through it. I used namecheap for mine and this is what I had to do. Once I navigated to my domain (where you have all the options for what to do next with your domain), I then had to click on "All Host Records" along the left. I imagine whatever service you're using you'll find a similar link to your host. So anything that says 'host', click on until you get to a page that has 

* Host Name
* IP Address/URL
* Record Type

Something that looks like that. Under the IP Address column put in these two IP Addresses ([provided by Github](https://help.github.com/articles/tips-for-configuring-an-a-record-with-your-dns-provider))

* 192.30.252.153
* 192.30.252.154

Then for record type you can select `A (Address)` for both. Be sure to save these changes. For `Host Name` it probably already has `@` and `www`. This just means your site can be found at both example.com and www.example.com. 

Once your CNAME file is pushed to Github and you've added the IP Addresses to your DNS provider, you should be able to see your site live after 10 minutes or so. 

####Subdomains
If you're using a subdomain (like blog.example.com) [Github has a reference](https://help.github.com/articles/about-custom-domains-for-github-pages-sites#subdomains) for that. They actually recommend always using a subdomain, but that's not always logical.

With these [Jekyll tutorials](/jekyll) you should be all set with a blog! I encourage you to continue reading the Jekyll documentation as these tutorials certainly weren't exhaustive. But hopefully now you have a better idea of how to get around Jekyll and can actually understand what they're talking about. Hope it helped!