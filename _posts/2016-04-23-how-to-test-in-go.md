---
layout: post
title: "How to Test in Go"
description: "Testing in Golang"
tags: [Golang, TDD, Go Testing]
image:
  background: bg4.png
comments: true
share: true
---
Let's test some Go!

For the past few weeks I've been teaching myself some Golang. I have to say, I like it. It's no Ruby in regards to ease of writing, but for a statically typed language, the learning curve is not too steep. 

This post will not go into the semantics of how to write Go code, but how to test it. I found the testing section in Go's [How to Write Go Code](https://golang.org/doc/code.html#Testing) to be a great way to set things up. So I did some of the practice problems from [App Academy](http://prepwork.appacademy.io/coding-test-2/practice-problems/) and did some TDD with Go's method. I thought I'd share what I found.

You can find all my tests (and Go solutions) at [this repo](https://github.com/trevordjones/app_academy_golang). 
Let's look at an easier one first:

{% highlight go linenos%}
package app_academy

import "testing"

func TestNoRepeats(t *testing.T) {
    cases := []struct{
        log string
        beginYear int
        endYear int
        expected []int
    } {
        {"it returns a no repeat year", 1234, 1234, []int{1234}},
        {"it does not return a repeat year", 1123, 1123, []int{0}},
        {"it returns only those years that have no repeated digits", 1980, 1989, []int{1980, 1982, 1983, 1984, 1985, 1986, 1987}},
    }
    
    for _, c := range cases {
        t.Log(c.log)
        noRepeats, err := NoRepeats(c.beginYear, c.endYear)
        for i := 0; i < len(c.expected); i++ {
            if err == nil {
                if noRepeats[i] != c.expected[i] {
                    t.Errorf("noRepeats equals %d, want %d", noRepeats[i], c.expected[i])
                }
            }
        }
    }
}
{% endhighlight %}

The hardest part of all of this is understanding how `cases` is working. We're assigning a variable `cases` to hold a struct which is made up of:

* what we want to log
* a starting year
* an ending year
* and the expected output

Each of these is assigned a type. Right after we declare it, we initialize it. That's why the `{}` immediately follows. Inside of here, we list everything out in the same order as what is assigned in the `cases` struct.

Next we perform the actual tests. Since cases is a struct, we can loop through it. `_` is the index, which we won't be using, and `c` is each case we're going to look at. We'll start first by logging to our terminal what we are testing. Next, we assign a variable to the return value of the function we wrote. As arguments to this function, we assign the case's `beginYear` and `endYear`. Next we iterate through the expected output, which is `c.expected`. Matchup what you get from `noRepeats[i]` and `c.expected[i]` and throw an error if they do not match up! Adding any other test cases is just a matter of adding to the `cases` struct. No additional code or logic is necessary.

Here's one that's a bit more complex in setting up the `cases` struct:

{% highlight go linenos %}
package app_academy

import "testing"

type Letters map[string]int

func TestLetterCount(t *testing.T) {
    cases := []struct{
        log string
        input string
        expected Letters
    }{
        {"it handles a simple case", "cat", Letters{"c":1, "a":1, "t":1}},
        {"handles multiples of the same letter", "dog", Letters{"d":1, "o":1, "g":1}},
        {"handles a multi-word case", "cats are fun", Letters{"a":2, "c":1, "e":1, "f":1, "n":1, "r":1, "s":1, "t":1, "u":1}},
    }
    for _, c := range cases {
        t.Log(c.log)
        countedLetters := LetterCount(c.input)
        for key, value := range countedLetters {
            if value != c.expected[key] {
                t.Errorf("value is %d, want %d", value, c.expected[key])
            }
        }
    }
}
{% endhighlight %}

The expected output of the `LetterCount` function is a map, and getting this to work well took a bit. I'm still new to Go so it wasn't immediately obvious how to assign the map to a struct. I'll let you look through this and work through how it's setup and see if you can reproduce it.

In the end, with a set up like this, you really just need to know how to set up your `cases` struct. You'll need something to log and something expected. The other options will depend on what kind of function/method you are testing. Then when you test, you just iterate through `cases` and throw an error when you come across something that wasn't expected. And the more verbose you are about what went wrong, the better you can debug.