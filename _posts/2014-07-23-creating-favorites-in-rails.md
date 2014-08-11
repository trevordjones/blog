---
layout: post
title: "Adding Ability to Favorite to Your Rails App"
description: "Creating the right associations for favoriting"
tags: [Ruby on Rails, Rails controller, Rails views, join table]
image:
  feature: abstract-9.jpg
comments: true
share: true
---

This was something I could not find anywhere - apparently people just 'know' how to do it. 

I didn't and I couldn't find anything that taught you how. But I have something now and you can take a look. I'll have a few posts on how your users can 'favorite' in your website. It works great for any kind of social network or if they want to follow certain topics.

###What kind of association is it?
This post will go over the association we need in our database. First you need to decide what kind of association you are going to have with this ability of users to favorite. You probably have two models, as User model and the model the user can favorite. For this example, we'll do a team. Say you want users to be able to follow certain sports teams which means you have something like a Team model. If the two can be directly joined together, then you most likely need a [has_and_belongs_to_many association](http://guides.rubyonrails.org/association_basics.html#the-has-and-belongs-to-many-association). Feel free to read through that document to learn more about associations, like 'has_many :through'. If you don't understand everything, that's ok.

For our case, it will be a has_and_belongs_to_many association. For this, we will need a join table. A join table is simply a way to track an association between two other tables. It 'joins' them together. 

To start, we'll make a table inside our Rails app called teams_users. Go ahead and create a migration by going to your terminal - run 
	
	rails generate migration CreateJoinTableForUsersTeams

Head over to your newly created migration file and use code similar to this:

{% highlight ruby%}
class CreateJoinTableForUsersTeams < ActiveRecord::Migration
  def change
    create_table :teams_users, id: false do |t|
      t.integer :teams_id
      t.integer :user_id
      end
    end
  end
{% endhighlight %}

Once you've filled out your migration file, head back to the terminal and run

	rake db:migrate

If you check your database now and refresh you should see a table called 'teams_users'. Perfect, now we can create our relationships with these models.

Open up your 'user.rb' file under the 'models' folder. Right underneath the class write 	

	has_and_belongs_to_many :teams	

Now open up your 'team.rb' file and write

	has_and_belongs_to_many :users

Now our relationshihp is set up. If you want to see how this works, open up your Rails console in the terminal. Run something similar to the following code (this is assuming you have both a user and an some other Model in your database):
	
	u = User.first
	t = Team.first
	u.teams << t
	u.save
	
With this, you're essentially joining the id for the team you selected (Team.first) with the id of the user you selected (User.first) and set them equal to variables so you could store them. Then if you just run `u.teams` it will show you all the teams associated with that user (User.first since you set it = to u). With `u.teams << t` you're putting that team inside the join table. Recall that `<<` stores an object into an array. Then you save it and head back to your 'teams_users' table and refresh. You'll see that 'Team.first' and 'User.frst' are together. 

Ok, now your database knows that these two models are associated and you can now show them in your website.

###Next steps
We'll need:

* [a proper route so users can view their favorites]({% post_url 2014-08-11-rails-routes-for-your-favorites %})
* a favorites controller
* a favorites model
* a favorites view
* and a button that will trigger the action to put data in the join table we just created
