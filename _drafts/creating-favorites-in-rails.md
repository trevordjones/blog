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
First you need to decide what kind of association you are going to have with this ability of users to favorite. You probably have two models, as User model and the model the user can favorite. For this example, we'll do a team. Say you want users to be able to follow certain sports teams which means you have something like a Team model. If the two can be directly joined together, then you most likely need a [has_and_belongs_to_many association](http://guides.rubyonrails.org/association_basics.html#the-has-and-belongs-to-many-association). Feel free to read through that document to learn more about associations, like 'has_many :through'. If you don't understand everything, that's ok.

For our case, it will be a has_and_belongs_to_many association. For this, we will need a join table. A join table is simply a way to track an association between two other tables. It 'joins' them together. 

If you know what one is, let's continue. We'll make a table inside our Rails app called teams_users. Go ahead and create a migration but going to your terminal - run 
	
	
	rails generate migration CreateJoinTableForUsersTeams

Head over to your newly created migration file and use code similar to this:

{% highlight ruby %}
class CreateJoinTableForUsersTeams < ActiveRecord::Migration
  def change
    create_table :players_users, id: false do |t|
      t.integer :player_id
      t.integer :user_id
      end
    end
  end
{% endhighlight %}

Once you've filled out your migration file, head back to the terminal and run

	rake db:migrate

If you check your database now and refresh you should see a table called 'players_users'. Perfect, now we can create our relationships with these models.

Open up your 'user.rb' file under the 'models' folder. Right underneath the class write 	

	has_and_belongs_to_many :teams	

Now open up your 'team.rb' file and write

	has_and_belongs_to_many :users

Now our relationshihp is set up. If you want to see how this works, open up your Rails console in the terminal. Run something similar to the following code (this is assuming you have both a user and a team in your database):
	
	u = User.first
	t = Team.first
	u.teams << t
	u.save
	
With this, you're essentially joining the id for the team you selected (Team.first) with the id of the user you selected (User.first) and set them equal to variables so you could store them. Then if you just run `u.teams` it will show you all the teams associated with that user (User.first since you set it = to u). With `u.teams << t` you're putting that team inside the join table. Recall that `<<` stores an object into an array. Then you save it and head back to your 'teams_users' table and refresh. You'll see that 'Team.first' and 'User.frst' are together. 

Ok, now your database knows that these two models are associated and you can now show them in your website.

###Now it's time to create the ability to favorite
Create a controller - I named mine 'favorites' but name it what you want and remember to make it plural:

	rails g controller favorites

Now in your 'favorite.rb file you'll want to input code similar to this:
{% highlight ruby linenos%}
class FavoritesController < ApplicationController
  def index
    @favorites = current_user
    @fav_leagues = current_user.leagues
    @fav_teams = current_user.teams
    @fav_players = current_user.players
  end
  
  def show
    if user_signed_in?
      @favorites = current_user
      @fav_leagues = current_user.leagues
      @fav_teams = current_user.teams
      @fav_players = current_user.players
    end
  end

  def create
    favorite = Favorite.new(params[:type], current_user,    params[:id])
    favorite.add_favorite!
    redirect_to(:back)
  end

  def destroy
    
  end

end
{% endhighlight %}

Substitute your models appropriately and you'll have a controller where users can now favorite on your site!

###Show your favorite button

But now you need a place for them to favorite. In your views create a 'show.html.erb' that corresponds with your 'show' action in the controller. Inside the 'show' view you would put in a 'form_tag' like so:

{% highlight ruby linenos%}
<%= form_tag("/favorites", method: "post") do %>
    <%= hidden_field_tag :id, @team.id %>
    <%= hidden_field_tag :type, "Team" %>
    <%= submit_tag "Favorite", class: 'your_class'%>
<% end %>
{% endhighlight %}
  
Place this code in your site where you want the favorite button to appear. You can reference the [Form Tag Helper](http://api.rubyonrails.org/classes/ActionView/Helpers/FormTagHelper.html#method-i-submit_tag) for Ruby on Rails to see all of your form_tag options.

So now when you go to your show page you'll see the favorite button. Click it and then check the join table in your database. Your user_id and the team_id (whatever you favorited) should now be listed side by side. Now you have an association! 

I'll be writing up another post shortly to show you how you can then display a user's favorites when they are logged in.