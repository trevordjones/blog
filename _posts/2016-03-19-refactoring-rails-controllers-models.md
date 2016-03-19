---
layout: post
title: "Refactoring Models and Controllers"
description: "Steps in refactoring your controllers and models"
tags: [Ruby, Rails, Refactoring]
image:
  feature: abstract-5.jpg
comments: true
share: true
---

Let's reactor the Rails Models and Controllers.

This is part two of how to start refactoring your Rails app. [The first post was about refactoring logic out of the view]({{ site:url }}/refactoring-rails-views), since it doesn't really belong there. The next logical place to look at refactoring is the controller and the model. I'm doing both because we can actually refactor the controller in such a way that our model remains largely untouched.

We all know that actions inside the controller can sometimes get bloated to 20 lines or more. You have tons of conditional logic as well as creating, updating,  and rendering. It can get overwhelming fairly quickly. So you treat the controller like the class it is and create other methods to deal with the logic. This is a good next step - you're whittling down the number of lines your action has and with good method names you can make it quite clear what each step is doing. But pretty soon, your controller is large, containing 10-15 different methods, none of them having to do with the actual actions of the controller.

So the next step developers take is refactoring to the models. After all, you seem to always hear 'Fat models, skinny controllers'. But should you be doing that? Should logic that really has nothing to do with the model really be in the model? Just because it's convenient, doesn't mean it should be done.

So if not the model and not the controller, where should the logic go? Enter action/service classes. Action classes are my favorite and are perfect for taking care of that pesky logic that doesn't have a home. Let's work through an example.

This is a basic, quick example which is not normally the case. If you need to resort to action classes you likely have a complex app. But for our purposes and the sake of time, we'll make it simple.

Suppose we have a list of companies and you as a user want to put the company in your profile. A basic model set up would be:

{% highlight ruby linenos%}
class Company
  has_many :portfolio
  has_many :users, through: :portfolios
end
	
class User
  has_many :portfolios
  has_many :companies, through: :portfolios
end
	
class Portfolio
  belongs_to :company
  belongs_to :user
end
{% endhighlight %}
	
In our database, we have a list of companies. So the controller for creating a portfolio would look like:

{% highlight ruby linenos%}
class PortfoliosController < ApplicationController
  def create
    Portfolio.create(user_id: current_user.id, company_id: params:company_id)
    flash[:notice] = "Portfolio saved"
    redirect_to portfolio_new_path
  end
end
{% endhighlight %}
	
This is very straightforward, and if this is all that is needed, then we're good. We don't render any errors here because we assume there will be a `company_id` (which we look at below). But what if we also want to allow the users to create a company if it doesn't exist in the database? Our controller would need to check if there is a company. If there is not, we need to create the company, then create the portfolio. We also need to do checks on the company to make sure it's valid. For instance, we can't create it if the user didn't provide a name. This becomes a little messier.

{% highlight ruby linenos%}
class PortfoliosController < ApplicationController
  def create
    company = Company.find_or_create_by(company_params)
    if company.valid?
      Portfolio.create(user_id: current_user.id, company_id: params:company_id)
      redirect_to portfolio_new_path
    else
      flash[:errors] = company.errors.full_messages
      render :new
    end
  end
end
{% endhighlight %}

As I said, this is a basic example and you'd probably be fine with this code in the controller. But often times, you need to introduce more logic if the requirements keep getting added. Like, what if a company shouldn't be saved if the portfolio is invalid? Well then you have to wrap the whole thing in a transaction and then have a rescue to show what the errors are. And what about the name? We need to have certain requirements for names, like they should be capitalized. And what if the user enters Amazon as the company but we already have Amazon.com, Inc? I don't believe `find_or_create_by` will be able to pick up that they are the same company. We would need a general search, like `Company.where("lower(name) LIKE ?", "%#{params[:name]}%")`.

One step we can take is refactoring this into it's own method. 

{% highlight ruby linenos%}
company = create_company
	
def find_or_create_company
  company = Company.where("lower(name) LIKE ?", "%#{params[:name]}%")
  if company.nil?
    company_params[:name].capitalize!
    company = Company.new(company_params)
  end
  company
end
{% endhighlight %}

Then in our `create` action, we just need to set `company = find_or_create_company`

Again, this would probably be just fine. That extra method isn't taking up much space. Until we get more requirements. For brevity's sake however, I won't go over any other requirements or any other methods that could be created in the controller. Instead, I'll show you how to refactor this in such that any new requirements you get, will most likely be easily taken care of without adding more logic inside the controller.

Let's add an action class. You can do so in your project by creating an `actions` directory inside the `app` directory. Place your file here and name it the same name as the action class (like the models and controllers are named). Here's what the rest of the code could look like.

{% highlight ruby linenos%}
class CreateCompanyPortfolio
  attr_accessor :company_params, :portfolio_params, :current_user
  
  def initialize(company_params, portfolio_params, current_user)
    company_params[:name].capitalize!
    @company_params = company_params
    @portfolio_params = portfolio_params
    @current_user = current_user
  end
  
  def create_portfolio
      ActiveRecord::Base.transaction do
        company = find_or_create_company
        company.save!
        portfolio = Portfolio.create!(user_id: current_user.id, company_id: company.id
      end
    company
  end
  
  def find_or_create_company
    company = Company.where("lower(name) LIKE ?", "%#{company_params[:name}%")
    company = Company.new(company_params) if company.nil
  end
end
{% endhighlight %}
	
Then controller would simply be:

{% highlight ruby linenos%}
class PortfoliosController < ApplicationController
  def create
    company = CreateCompanyPortfolio(company_params, portfolio_params, current_user).create_portfolio
    if company.valid?
      redirect_to portfolio_new_path
    else
      flash[:errors] = company.errors.full_messages
      render :new
    end
  end
end
{% endhighlight %}
	
You may wonder, this cleaned up the controller a little, but it seemed to add a lot more code. True. As I said, this was a basic example. But imagine if you have further requirements that require other checks or inserting more data, like if we needed to create a notification of some kind. Now, instead of adding any more code to the controller, that code can be added to the action class. Build out that action class as you need and keep the controller *and* the model skinny. Responsibilities of classes remain singular and leave only logic that is supposed to exist in those controllers and models!