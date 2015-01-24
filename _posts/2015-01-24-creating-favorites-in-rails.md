---
layout: post
title: "Adding Ability to Favorite to Your Rails App"
description: "Creating a 'Favorites' Controller and View"
tags: [Ruby on Rails, favorites controller]
image:
  feature: abstract-9.jpg
comments: true
share: true
---

This was something I could not find anywhere - apparently people just 'know' how to do it. 

I didn't and I couldn't find anything that taught you how. But I have something now and you can take a look. This is how your users can 'favorite' in your website. It works great for any kind of social network or if they want to follow certain topics.

###What kind of association is it?
First you need to decide what kind of association you are going to have with this ability of users to favorite. You probably have two models, a User model and the model the user can favorite. For this example, we'll do a Team. You want users to be able to follow certain sports teams which means you have something like a Team model. If the two can be directly joined together, then you most likely need a [has_and_belongs_to_many association](http://guides.rubyonrails.org/association_basics.html#the-has-and-belongs-to-many-association). Feel free to read through that document to learn more about associations, like 'has_many :through'. If you don't understand everything after reading it, that's ok. We can still move on.

For our case, it will be a has_and_belongs_to_many association. I chose this instead of has_many :through because this requires a third model (which could be Favorite) and it would only be used to create the association. It wouldn't actually hold any data - not in our case. If it has no other purpose, we can forego it. For our chosen association, we will need a join table. A join table is simply a way to track an association between two other tables. It 'joins' them together. 

If you know what one is, let's continue. We'll make a table inside our Rails app called 'teams_users'. Go ahead and create a migration by going to your terminal - run 
	
	
	rails generate migration CreateJoinTableForUsersTeams

Head over to your newly created migration file and use code similar to this:

{% highlight ruby %}
class CreateJoinTableForUsersTeams < ActiveRecord::Migration
  def change
    create_table :teams_users, id: false do |t|
      t.belongs_to :team
      t.belongs_to :user
      end
    end
  end
{% endhighlight %}

Once you've filled out your migration file, head back to the terminal and run

	rake db:migrate

If you check your database now (schema.rb file in the db directory) and refresh you should see a table called 'teams_users'. Perfect, now we can create our relationships with these models.

Open up your 'user.rb' file under the 'models' folder. Right underneath the class write 	

	has_and_belongs_to_many :teams	

Now open up your 'team.rb' file and write

	has_and_belongs_to_many :users

Now our relationshihp is set up. If you want to see how this works, open up your Rails console in the terminal. Run something similar to the following code (this is assuming you have both a user and a team in your database):
	
	user = User.first
	team = Team.first
	user.teams
	user.teams << team
	user.save
	
With this, you're essentially joining the id for the team you selected (Team.first) with the id of the user you selected (User.first) and set them equal to variables so you could store them. Then if you just run `user.teams` it will show you all the teams associated with that user. With `user.teams << team` you're creating a record in the join table. Recall that `<<` stores an object into an array - basically what we're doing. Then you save it and head back to your 'teams_users' table and refresh. You'll see that 'Team.first' and 'User.frst' are the first entries in your table. 

Ok, now your database knows that these two models are associated and you can now show all the teams associated with the specific user on your website.

###Now it's time to create the ability to favorite
If you don't have controllers yet, create one for teams and one for users. 

	rails g controller teams
	rails g controller users

Now in your 'teams_controller.rb' file you'll want to input code similar to this:
{% highlight ruby linenos%}
class TeamsController < ApplicationController

  def index
  	#show all the team on the index page
    @teams = Team.all
  end
  
  def show
    @team = Team.find(params[:id])
  end
  
  #create our own favorite action
  def favorite
  	team = Team.find(params[:id])
  	current_user.teams << team
  end
  
end
{% endhighlight %}

The `current_user` method is assuming you have the Devise gem set up in your model. If you're just doing this on a simple test app and don't want to set up Devise, you can set `current_user = User.first`. 

You'll need to make an adjustment in your routes.rb file so it looks something like this:
{% highlight ruby linenos%}
  
  post 'teams/:id/favorite' => 'teams#favorite

{% endhighlight %}

Here we are creating a route where we can make a request with our `favorite` action. Now a user just needs to click on a team to go to its show page and we'll have our favorite button there!

All this is assuming you have records created for at least one user and one team in your database. If not, fire up your Rails console and create some.

###Show your favorite button

In your 'views' folder under 'teams' create a 'show.html.erb' that corresponds with your 'show' action in the controller. Inside the 'show' view you would put in a 'form_tag' like so:

{% highlight ruby linenos%}
<%= form_tag(controller: "teams", action: "favorite", method: "post") do %>
    <%= submit_tag "Favorite"%>
<% end %>
{% endhighlight %}
  
Place this code in your site where you want the favorite button to appear. You can reference the [Form Tag Helper](http://api.rubyonrails.org/classes/ActionView/Helpers/FormTagHelper.html#method-i-submit_tag) for Rails to see all of your form_tag options.

So now when you go to your show page you'll see the favorite button. Click it and then check the join table in your database. Your user_id and the team_id should now be listed side by side. Now you have an association! You can also check it out in the Rails console and do the code that was written further.

Right now this doesn't have any flashes, which wasn't the point of the post. You'd definitely want to include those and put them in your view so the user knows the action was successful.

I'll be writing up another post shortly to show you how you can then display a user's favorites when they are logged in.