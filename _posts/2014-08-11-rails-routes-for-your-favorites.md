---
layout: post
title: "Favorites: Setting up your Views in Rails"
description: "Creating the proper routes to show a user's favorites"
tags: [Ruby on Rails, Rails routes, Rails controller, Rails views]
image:
  feature: abstract-8.jpg
comments: true
share: true
---

Showing your users' favorites:

This is a continuation of my [favorites post]({% post_url 2014-07-23-creating-favorites-in-rails %}) where I showed you how to create the appropriate tables in your database so users can favorite . . . whatever. In my case, it was favoriting certain leagues and teams for soccer. But it can be a 'like' button or anything like that.

Now if you want their favorites to show up on a certain page, here are a couple ways to do that. In this post I'll go over the routes file and in later posts I'll show you what the controller and model could look like (I'm sure there are several ways to code this up). 

##Routes file
Create a place for your favorites to live in your `routes.rb`.  You can do a couple things here. I wanted my URI to look like `favorites/leagues` but I could have also made it `leagues/favorites`. Here is how you would do `leagues/favorites`. 

####Namespace
You can make a new namespace for each object a user can favorite. This probably requires the most code, but you can:

{% highlight ruby%}
namespace :route do
  resources :favorites
end
{% endhighlight %}

Replace 'route' with the route that a user can favorite (so it would be `:leagues` for me). With this one, you'd have to do it with each object a user can favorite if you have routes set up for each. I'd have to do two, one for leagues and one for teams, so I didn't use this.

There is also a way to do it without any prefixes but I would imagine you only want to use this if there is only one object a user can favorite. I have two objects, leagues and teams, so having a prefix of `leagues/` or `teams/` before the `/favorites` is handy because it shows the user where he or she is on the site. But to get rid of the prefix, you would:

{% highlight ruby%}
scope module: 'route' do
  resources :favorites
end
{% endhighlight %}

I would show you what this gives you but I actually encourage you to see for yourself. Put it in your routes file and then in your terminal run `rake routes`. It's associated with the route that you specified but as you can see, it's not included in the URI Pattern but it is in the Controller#Action. 

####Create a favorites route

I created a whole new favorites route. I set it up like this:

{% highlight ruby%}
resources :favorites
get '/favorites/leagues' => 'favorites#show'
get '/favorites/teams' => 'favorites#show'
{% endhighlight %}

The `resources :favorites` is setting up all of my controller actions, like create, edit and destroy. Then I just add to the show action so users can get to leagues, teams or players and know which part of the site they are on by the URI. 

This way also made it so I only needed one create, edit, destroy, new, and update for favoriting. Using the first way would mean you create each action for each object you favorite. Again, if you only have one object a user can favorite, then the first way works just fine. OR, if you prefer to have `route/favorites` instead of `favorites/route` then the first way is for you too.

But I prefer this. I can set up all the code that is required for favoriting inside one controller and one model, both names `favorites_controller.rb` and `favorite.rb`.Here's a list of the steps for adding the ability to favorite:

* [appropriate join tables]({% post_url 2014-07-23-creating-favorites-in-rails %})
* proper route so users can view their favorites
* favorites controller
* favorites model
* favorites view
* a button that will trigger the action to put data in the join table we just created


