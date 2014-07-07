---
layout: post
title: Change the Default Routes on Devise
description: "Instructions for chaning the default routes on Devise"
tags: [Ruby on Rails, Devise]
image:
  feature: abstract-4.jpg
comments: true
share: true
---

## How to change the default Devise routes
If you are trying to change the default routes of Devise from '/users/sign_in' or '/users/sign_out' to something more like '/login' or '/logout' you've found out how.

This problem was very frustrating but very simple to solve. Don't look at stackoverflow for this one - those answers are way to complicated for what you are trying to do. Devise has good documentation on it but it was very difficult to find: [Change the default sign_in and sign_out routes](https://github.com/plataformatec/devise/wiki/How-To:-Change-the-default-sign_in-and-sign_out-routes). 

Just look at the last section, 'The simple way to do it':
`devise_for :users, :path => '', :path_names => {:sign_in => 'login', :sign_out => 'logout'}`

You're just changing the path names. So if you want to change the '/users/sign-up' route as well, just include it after 'logout', so:
`devise_for :users, :path => '', :path_names => {:sign_in => 'login', :sign_out => 'logout', :sign_up => 'sign-up'}`. The default path is listed first and it points to (=>) the path you want (it also goes ahead and takes out the 'users' part of the url as well).  If you need the default routes, they are:

{ %raw% }
new_user_session_path	 GET	 /users/sign_in(.:format)	 devise/sessions#new
user_session_path	 POST	 /users/sign_in(.:format)	 devise/sessions#create
destroy_user_session_path	 DELETE	 /users/sign_out(.:format)	 devise/sessions#destroy
user_password_path	 POST	 /users/password(.:format)	 devise/passwords#create
new_user_password_path	 GET	 /users/password/new(.:format)	 devise/passwords#new
edit_user_password_path	 GET	 /users/password/edit(.:format)	 devise/passwords#edit
PATCH	 /users/password(.:format)	 devise/passwords#update
PUT	 /users/password(.:format)	 devise/passwords#update
cancel_user_registration_path	 GET	 /users/cancel(.:format)	 devise/registrations#cancel
user_registration_path	 POST	 /users(.:format)	 devise/registrations#create
new_user_registration_path	 GET	 /users/sign_up(.:format)	 devise/registrations#new
edit_user_registration_path	 GET	 /users/edit(.:format)	 devise/registrations#edit
PATCH	 /users(.:format)	 devise/registrations#update
PUT	 /users(.:format)	 devise/registrations#update
DELETE	 /users(.:format)	 devise/registrations#destroy
{ %endraw% }

Doesn't make sense - ask away below.