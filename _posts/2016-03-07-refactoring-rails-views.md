---
layout: post
title: "Refactoring Views in Rails"
description: "Refactor logic out of a Rails view"
tags: [Ruby, Rails, Refactoring]
image:
  background: bg8.png
  comments: true
share: true
---

One of the bigger struggles for newer developers on Rails is refactoring the MVC. What belongs in the Model, View and Controller. It can be a tough task. I'll focus first on what belongs in each and then how to refactor them. This will be 3 part series to help keep it concise and specific. I'll start with the view first and provide links to the other two.

###View
The view can easily get cluttered. It seems the easiest to put logic there since we can and since it's dealing directly with info the user is seeing. When I was first coding I found myself putting in `if else` like crazy. An recent example of mine where I could have easily done this is with a user photo and user avatar. I have a social network where a person viewing someone else's profile shouldn't see their photo, but their avatar if the two were not connected. Same goes with the name and anonymous username - but for now I'll just use the photo as the example.

I have a few pages that show a user's regular profile and anonymous profile. So that means I had a lot of `if else` in quite a few views. Something like:

	<% if user.connected? %>
	  <img src="<%= user.photo %>" />
	<% else %>
	  <img src="<%= user.avatar %>" />
	<% end %>
	
5 lines. Surely there's a better way!

And there is. This kind of logic doesn't really belong in the view. If you need to use any kind of Ruby in the view, it should be for things like:

* iterating through a list of objects
* calling an attribute on a Model object to show it's value (i.e, `current_user.full_name`
* Any kind of forms (`form_for`, `form_tag`)
* Rendering views

I believe that's the bulk of what would go in a view. Most everything else can fit elsewhere. Let's take a look where.

For the example above, one thing we could do is write a method in the `User` model. We could write it something like:

	def show_photo
	  connected? ? photo : avatar
	end
	
Then the view would be:
	
	<img src="<%= user.show_photo %>" />
	
This does a couple great things for us. One is now the logic is much cleaner. The code in the view is one line and the code in the model is one line (2 extra if you cound `def` and `end`. Also, this can be used across any view. Every single one. So now instead of 5 lines for every view, we have one line across every view and the associated model method.

Is this the best place for it? Some would argue no, others would argue yes. Die hards would say that logic that has nothing to do with the actual data does not belong in the model. That is typically what the model is for. So where else could it go?

A helper. If you did a `rails g model User` to get your model, I imagine you got a `UsersHelper` to go along with it. If not, go ahead and create this file inside your `helpers` directory called `users_helper.rb` This file can now hold most if not all the logic that is in our view. It can deal with any kind of model, but normally to keep things organized you would only put `User` specific logic here.

Can we write the same method in here as we did in the `User` model? No. Our `user` object is not an instance of `UsersHelper`, so the attributes on `user` can't be used the way we did with the above `show_photo` method. What we can do, is pass in the `user` object as an argument to the method.

	def show_photo(user)
	  user.connected? ? user.photo : user.avatar
	end
	
And then in the view
	
	<img src="<%= show_photo(user) %>" />
	
This same thing can be done with any kind of `if else`, which I think is the most common kind of logic that developers place in the view. Do the checking inside a helper and inside the method, return whatever needs to be seen by the user. In this particular case, I feel it's perfectly fine to place this inside the `User` model, however there are many times the logic should not go in there - perhaps because it has nothing to do with the actual model. 