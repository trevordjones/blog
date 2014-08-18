---
layout: post
title: "Linking Blog Posts in Jekyll"
description: "Link between your blog posts with post_url"
tags: [Jekyll, how to blog with Jekyll, markdown]
image:
  background: bg5.jpeg
comments: true
share: true
---

Linking to your blog posts.

The [Jekyll documentation](http://jekyllrb.com/docs/templates/#post-url) is fairly clear on this - for whatever reason, though, it wouldn't work for me for the longest time. I just kept trying it until one time, it worked. If you're struggling with it, be sure Jekyll is up to date and the github pages gem is up to date in your gemfile. I've looked through the issues on Github and I know there were problems with this at one time - if you find the answer, please share.

###post_url

For now, just make sure you're linking EXACTLY the way Jekyll says, that is:

	[Markdown in Jekyll]({$ post_url 2014-07-25-markdown-for-jekyll $})

'post_url' followed by the file name of your post. There is no file extension, no quotes, no connection between 'post_url' and the file name - exactly like this. AND, replace the '$' with '%'. I used '$' because if I used '%' it would have created the link and you wouldn't have seen how it works. VERY important.

###Problems linking
If you are having problems linking with the above syntax, you can use site:url. The syntax looks like this:

	[words to link]({ { site:url } }/file-name)


But you must make sure there are NO spaces between the brackets. I did it this way because I had to make sure it showed up on the page instead of rendering as my actual site url. This way if you ever do change your domain, your links will still work. The above syntax is preferrable, but if you can't get it to work, site:url works just fine.

####Next Steps
By now you should have your blog live through gh-pages, a post up, be able to link and are now ready to publish your blog using your purchased domain! Let's [go to that post]({% post_url 2014-08-18-custom-domain-with-github-pages %}) and finish getting your blog set up.