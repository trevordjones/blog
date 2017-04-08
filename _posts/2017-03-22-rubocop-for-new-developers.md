---
layout: post
title: "Using Rubocop as a New Developer"
description: "Should you be using Rubocop when you're just starting?"
tags: [Ruby, Rubocop]
image:
  background: bg5.jpeg
comments: true
share: true
---

Over the past almost 3 years now I've dealt a lot with new developers. At first I was one, then I TA'd for them for over a year, then I was a tech lead for them when they started an apprenticeship, then I was a teacher for a cohort over the summer, now I'm back to being a tech lead for the apprenticeship. So I feel that I have some experience regarding new developers.

One thing I've learned is not to baby them.

Ok, I know this sounds harsh. But the training wheels have to come off. These new developers need to learn sooner rather than later how to write clean, easy to reason about code. For their own sake, they must learn to do this. I think too often teachers are too caught up with helping the students learn to think like a developer that we forget to teach them to write code like a developer. Learning to think like a developer is probably the biggest and hardest step, especially for those not coming from any kind of tech/software background. But let me ask, how can you think like a developer with spaghetti code everywhere? How can you reason about your code when it was barfed up on the screen?

New developers tend to focus on working code. It works, so why bother with it? And I believe as teachers/mentors, we see that it's working and are so relieved, we leave it at that. This is a disservice to them. Not only can cleanly written code help them in finding a job, it can help them learn how to program. The earlier they can learn the rules of the trade, the better off they will be.

My first 18 months as a developer, no one taught me this. I was just flying by the seat of my pants, making up my own styles, trying my best to learn how to write clean code. I didn't know about this thing called [Rubocop](https://github.com/bbatsov/rubocop). I heard of "linting" but no one really told me what is was and so it didn't seem important enough for me to look up.

How I wish I had. I started a new job back in September and my boss is extremely pedantic. At first, I thought this was annoying. My code was fairly clean, it made sense, it worked - why bother with it? But as I started following the Rubocop style guide, my code kept looking better and better. It was clean and it felt so good to write and so good to read. I started thinking more clearly about the problems and how to fix them. I started remembering methods better and how to use them. In short, it's been a huge help to me and I can't believe it took me two years to get to that point.

Don't let that be you.

### Setting up Rubocop

If you just finished a bootcamp or are still in one, start being strict with yourself. Start learning the rules and start following them. The best way to do that is with Rubocop and a solid linter. This is my setup:

* Atom as my text editor (duh, it's free and amazing)
* These packages from Atom
  * linter (a new version came out and it's awesome)
  * linter-ruby
  * linter-rubocop
* rubocop.yml file - if you don't have one, you can grab one [here](https://gist.github.com/trevordjones/c1978320b5e1afecc92a49d510c8b2fe).

Then in your settings for linter-rubocop you can put something like this in the command line `/path_to/.rbenv/versions/2.3.1/bin/rubocop --config /path_to/.rubocop.yml`

You run the `rubocop` command and pass in the path to where your `.rubocop.yml` file is. This section from the package tells you where you can find the path to your `rubocop` command.

Then sit back and let the magic begin. Write some code, see what the suggestions are, and then (and this is the important part) *actually take the suggestions!*. I know it take you longer to write code - but that is only short term. You will get better and better at coding if you're persistent with best practices. Just do it!
