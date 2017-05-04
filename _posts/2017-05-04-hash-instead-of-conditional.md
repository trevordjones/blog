---
layout: post
title: "Hashes Instead of Conditionals"
description: "How you can use hashes to clean up your conditionals"
tags: [Ruby, programming, refactor]
image:
  background: bg10.jpg
comments: true
share: true
---

Try Hashes in place of conditionals!

So this implementation isn't what you should do 100% of the time. But in a lot of cases, you can dry up your code/make it cleaner by doing some logic with a hash instead of a bunch of `if` statements. The example I am thinking of is the Raindrop exercise. I'm familiar with it from Exercism but I'm sure it didn't originate there. It's pretty much the same idea as FizzBuzz. Here's one common implementation:

{% highlight ruby linenos%}
class Raindrops
  def self.convert(drop)
    rain = ''
    rain << 'Pling' if (drop % 3).zero?
    rain << 'Plang' if (drop % 5).zero?
    rain << 'Plong' if (drop % 7).zero?
    if rain.empty?
      drop.to_s
    else
      rain
    end
    # Or
    # => rain.empty? ? drop.to_s : rain
  end
end
{% endhighlight %}

Or you could make it longer by nesting a bunch of `elsifs`. Is there anything wrong with the implementation? Nope. It works. It's clean. Developers can understand it. Maybe it's a little wet - there are three lines which are more or less identical. And what if we wanted to add three more? Divisible by 8, or 11, or 13. We'd have to keep adding more lines and setting up more conditionals, all of which look pretty much the same. Turns out it's not the most robust code - we have to add more code to the method as we receive more conditions.

Is that important in a simple exercise like this? No. But it could be in a production project when you're working with several developers and have several unknowns for what the end result really should be or what is going to be plugged into it.

Let's try doing this with a Hash instead:

{% highlight ruby linenos%}
class Raindrops
  class << self
    RAINDROPS = { 3 => 'Pling', 5 => 'Plang', 7 => 'Plong' }.freeze

    def convert(drop)
      rain = ''
      RAINDROPS.each { |k, v| rain += v if (drop % k).zero? }
      rain.empty? ? drop.to_s : rain
    end
  end
end
{% endhighlight %}

`RAINDROPS` is a constant because we do not change it at all in the execution of our code. When we iterate through it, we check the key against the drop amount to see if it's a factorial. If so, we add the value for that key to the `rain` variable. Now what happens if we need to add more options to check against? We simply add it to the `RAINDROPS` hash. Our `convert` method need never change unless the requirements change.

Try it out with FizzBuzz!
