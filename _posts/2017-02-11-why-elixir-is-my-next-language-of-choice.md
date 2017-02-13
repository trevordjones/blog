---
layout: post
title: "Why Elixir is My Next Language of Choice"
description: "Elixir Programming Language"
tags: [Elixir]
image:
  background: bg1.jpeg
comments: true
share: true
---

I'm Moving Forward with Elixir

For almost 3 years now I've been coding in Ruby and JavaScript. I love Ruby, I really do. It's precise, it's beautiful, it has powerful features - and it has Rails. JavaScript? I like the language - I wouldn't choose it to write server side code though. I mostly like it because of how "snappy" I can make my web app. ES6 made it much more fun to code with and when you combine it with Vue.js you get pure developer happiness. More so than with React IMHO. I loved my first month with Vue.js and didn't hate my first month with React. If you haven't yet, please do yourself a favor and [go give it a try.](https://vuejs.org/)

What does this have to do with Elixir? Nothing. Just wanted to spout my views on two current languages. But going into the future, I believe Elixir has the best chance out there to overtake Ruby. JS will obviously be super relavant always since it's the language of choice for the browser.

I see two big contenders for server side language in the years to come - Elixir and Golang. In this post I will not in anyway give the technical differences since I just don't know enough about either to do so. But based on the research I have done and the experience I've had with each to date, Elixir is the way I want to go and I'll explain why.

Golang is a great language. I have extremely limited experience with it - and that's for a reason. It was taking me too long to become productive with it. Gophers pride themselves on not using frameworks - but rather picking and choosing different libraries and making them coexist peacefully. That's well and good and all, but when it takes a person new to the language over a week to set up the DB and figure out how to set up the proper associations, it's just not worth it to me. I'm still fairly new with programming and don't have a hugely extensive background with it (as I mentioned, I'm only about 3 years in). But I feel like I'm at a point where with a solid couple weeks with a language I should be able to get somewhere with it.

I understand that a reliance on a framework can be crippling - maybe not crippling, but certainly a crutch. I do feel that it's important to learn the underpinnings of a framework - but I don't feel it's necessary to work without one. Why code the same thing over and over? Why make the same decisions? Or even worse, change decisions every time? Why not go with an approach that's tried and true and you know just works (ahem, Rails).

That really was my only problem with Golang - but it's a pretty big one for me. The documentation is there and it's great (when learning to code, I HATED docs that were either too arrogant or too lazy to write proper documentation for people to understand) and the support is there. It's growing in popularity and I don't believe you can go wrong by moving forward with it. But it's not for me.

Enter Elixir. Where have you been?! It's my own fault actually. I had the chance almost a year ago to start learning it and I chose to stick with Ruby (which isn't a bad choice, but sometimes I wish I picked up Elixir sooner). What an incredible language. Syntatically, it's beautiful, just like Ruby. I just feel elegant when I'm working with it. I've been working through the Exercism exercises and with these two methods:

{% highlight elixir linenos%}

def is_sublist?(_, []) do
  false
end

def is_sublist?(a, b) do
  if a == (Enum.chunk(b, length(a)) |> List.first), do: true, else: is_sublist?(a, tl(b))  
end

{% endhighlight %}

I was able to write the code for the sublist exercise. I won't explain it here, but it's something that would take more lines in either Ruby or JavaScript (perhaps even Go). [There's more to it than just this](https://github.com/trevordjones/exercism-elixir/blob/master/sublist/sublist.exs) - but these two methods do the bulk of the work.

It felt super weird to define a method with the same name twice, but once I saw the value in pattern matching it. Blew. My. Mind. Pattern matching and recursion are wonderful things that aren't used much in the Object Oriented world (recursion some, pattern matching I've never come across - if I did I didn't realize it). 

How long did it take me to solve it? About 15, maybe 20 minutes. And remember, I'm brand new to this language, so syntax is still a barrier to me. There's still so much about it I don't know. I mention that not to show that I'm some genius programmer (because I'm not, if that wasn't made clear) - but to highlight how crazy good Elixir is. With Golang, that would've taken me a full day.

As Chandler from Friends would say, 'Can I be any more productive with Elixir?' It's amazing. And another thing - documentation is first class in Elixir. It comes built in so you can easily add it to your own code. And their site and Hex docs are just awesome and super intuitive. And if this isn't enough, Elixir has a framework called Phoenix. Admittedly, I haven't been able to dig into Phoenix yet, but from what I've read, it's like Rails and can get you up and building in no time.

So if I can be productive with a language, be happy coding with that language, and have a framework in my toolbelt to then build something, then I want to use it. That's why I love Ruby. So then why even bother with Elixir if Ruby has it all? Because it doesn't quite have it all. Concurrency -- speed -- power. If Ruby lacks anything, it's those. True, you can always spin up more servers, but that's money out the door. [Real world example](http://www.techworld.com/apps/how-elixir-helped-bleacher-report-handle-8x-more-traffic-3653957/) - Bleacher Report moved from Ruby to Elixir. Their lead engineer said that with Ruby, they at times had to run 150 servers. With Elixir, they run 5. He said they probably only need 2. Even without that advantage - the lead engineer also said Elixir gave them a cleaner code base and *faster* development!

Do we all need something that can scale massively? No. 98% of the time, Ruby does great. But if I can work with a language where I am happy coding with it *and* it has a robust framework *and* it allows me to code faster *and* gives me a cleaner code base *and* provides faster performance...well, then it's just silly to not use it.

