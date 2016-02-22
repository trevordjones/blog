---
layout: post
title: "SRP Classes and Gilded Rose Kata"
description: "One way to refactor the Gilded Rose Kata"
tags: [Object Oriented Design, single responsibility classes, SOLID]
image:
  background: bg2.jpg
  comments: true
share: true
---
Refactoring the Gilded Rose Kata - Object Oriented Design Patterns

I've been trying to increase my Object Oriented design skills and someone recommended I look at the Gilded Rose kata. It's an interesting kata and definitely one I recommend as well. It's a refactoring kata - you're taking poorly written code and making it more truly line up with OO design. I've got my final product at [https://github.com/trevordjones/gilded\_rose\_kata](https://github.com/trevordjones/gilded_rose_kata)

I started by forking from [Jim Weirich's repo](https://github.com/jimweirich/gilded_rose_kata). I changed up his tests as they seem a bit dated and were super confusing themselves. It's a good exercise in test writing, so I suggest you start there. DEFINITELY do it before you touch any of the other code. You want to make sure all your tests are in the green before you start refactoring. If testing is not your thing, you can grab mine from my repo in the link above. Looking through and understanding the tests will also help you understand what the code is doing. It's super confusing. There are about 20 if statements you have to read through.

Once the tests were done and passing, I dug into refactoring the code. Since it was so dense with conditionals, I figured the easiest thing to do was to take this in stages. Refactoring would be a multi-step process. 

My first pass was just to reduce the number of conditionals. I analyzed what each `if` was doing and decided to make a method out of the code from the initial `if` to the `end`. This gave me 5 different methods to work with, one for each type of item. If you name the methods clearly, you'll then know what each `if` is doing just by reading the method name. Then when you update the item, it simply calls each method on the item, and each individual method takes care of updating the item.

But this still has it's limits. We still have to call all the methods every single time, despite what kind of item it is. This seems a bit wasteful.

Before I could go on to fixing that though, I wanted to continue making this more truly Object Oriented. So instead of using the `Struct.new` that they provide, and make it its own class. This class would then have an `initialize` and `update_quality` method on it. The `update_quality` would then handle calling the other 5 methods. So now we have a proper class, but still are executing too much code.

Well, with 5 different methods that are each handling a specific type of item, it seemed like the next logical step was to create a class for each item. If each item had its own class, then each item could have its own `update_quality` method on it. And, the important part, if the type of item is an instance of that class, then we no longer have to call our 5 different methods from the first refactoring.

That's probably the most important part from this. The code no longer has to run a conditional to find out what type the item is. If it's created as an instance of the appropriate class, we can simply call the specified `update_quality` on that instance. So `Normal`, `Sulfuras`, `AgedBrie`, `BackstagePass`, and `Conjured` are all there own classes with their own `update_quality` methods.

If we make each of these classes have their own `initialize` method, we see a lot of repeated code. We can dry it up by having the `initialize` method in the `Item` class we created earlier and then each of these can be subclassed from `Item`.

Perfect!

Now when we have a normal item, we call 

	normal = Normal.new(name, sell_in, quality) 

and whenever we need to update our normal item, we call 

	normal.update_quality 

It then runs only methods that are necessary for a normal item. Our code is now separated so each item type is responsible for itself, thus adhering to the S in SOLID. Each type of item can now take care of itself and doesn't care about any other item. And the developer can now understand what is happening for each item. 

(At this point it's also much easier to test, so for further practice, you can try refactoring the tests).

