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

Substitute your models appropriately and you'll have a controller where users can now favorite on your site! *Important Note* This will work if you have the Devise gem. That's where `if user_signed_in?` comes in to play, it's specific to Devise.

###Show your favorite button

But now you need a place for them to favorite. In your views create a 'show.html.erb' that corresponds with your 'show' action in the controller (but you probably already have this). Inside the 'show' view you would put in a 'form_tag' like so:

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