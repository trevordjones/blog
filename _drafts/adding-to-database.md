This post will teach you how to download data from your 
API to the MySQL database in Ruby on Rails.

It's tricky when you're new to everything but makes complete sense once you see it in action. The example I'll be giving you is putting soccer team data in my database (using MySQL) from two different API's. I get some data from one API but I have to resort to the other API to get the rest. 

If you found this post I assume you already know which API you're using and possibly already found a wrapper. If not, you should look to see if there is one. 

What you need to do is call your API inside your seeds.rb file, write up a create method (this stores the data in MySQL) and then rake db:seed in the terminal. Before we start, make sure you have your table set up with the appropriately named columns (which will I assume be based on the data you're pulling from the API).

This is an example of what it would look like in the seed.rb file using the XML Soccer API and xmlsoccer gem:

{% highlight ruby linenos%}
client = Xmlsoccer::Client(api_key: 'API-Key', api_type: 'Type')
teams = client.get_all_teams_by_league_and_season(league: 'English Premier League', season_date_string: '1415')

teams.each do |team|
  Team.create(:name => team["name"], :stadium => team["stadium"], :homepage => team[:"home_page_url"])
end

{% endhighlight %}

Let's take a closer look so you know what's going on and can apply it to your project. First, I'm making a call to my API. Either the API or your Ruby gem wrapper will give you details on how to call it. This is how I call using XML Soccer, not how you would call yours. I'm setting that to the variable 'client'. Then I use 'client' to get the teams in the English Premier League during the 2014-15 season and I set that to the variable 'teams'. Now 'teams' contains all the data about the English Premier League teams that XML Soccer gives me. 

Then you want to run your friend, the each method. It's a wonderful method. This will allow you to pull out specific information about each team. Next we'll want to use the create method - this is the method that will store the data to the database. So you call the appropriate model (Team) and then call the create method because now you'll be putting data in it. Now we need to select the info about each team that we want to put into the database *and* put it in the right column.

If the person who created your API or Ruby wrapper knew what he or she was doing, you're probably getting your data in a hash format. remember that we call hashes with the variable the hash is set to followed by ['hash key']. So in this case, my data is set to the 'team' variable (using the each method). I want to get the name of the team from the hash, which has the key 'name'. 

	[{location => "Liverpool" name => "Liverpool" nickname => "The Reds"}]
	
So I just call it with

	team["name"]
	
It could be different for each API, it just depends on how they display the data. So you need to figure out how to call specific data and use it in the each method with Model.create. You also want to make sure the data is put under the proper column. Hence :name => team["name"]. :name is the name of my column set aside for the team name. 

So it looks like 

	:column-name => variable-hash-is-stored-in["hash key"]

Once this is set up, run `rake db:seed` from your terminal and then check your database.

Then if you have another API and you want to update your current data, *not* add more rows to your database, you need to call the update method instead of the create method. You first find the right team and then update it. Now it would look like:

{% highlight ruby linenos%}

client = ESPN::Client.new(api_key: 'API-Key')
teams = client.teams(:soccer, "eng.1")

teams.each do |team|

  team = Team.find_by(:name => team["name"])

  team.update(:nickname => team["nickname"], :location => team["location"])

end
{% endhighlight %}

Something to keep in mind when using this is that *one* piece of data from both API's must match. This one piece of data is what you use in the find_by method. This will match up what you already have in the database with what you're going to put in it with the new API. I used the team name, as that is generally always the same. 

Hope this helps!