---
layout: post
title:      "Twin Tiers Cinderella "
date:       2020-04-20 00:05:34 +0000
permalink:  twin_tiers_cinderella
---


For my Ruby on Rails project I made an application Twin Tiers Cinderella, where coaches/users can register their teams, and players for the Cinderella Softball League in the Twin Tiers region located in Upstate New York.  With using Rails you still follow the main convention of MVC (Model, Views, Controllers) framework.  I set up my models of a user/coach, teams, players.  I implemented relationships/associations of my models.   Where the user has_many :players,and has_many :teams, through: :players.  The team has_many :players, and has_many :users, through: :players.  The player is the join table between the two, where is belongs_to :user, and belongs_to :team.
Making the database the player has both foreign keys of the user_id, and the team_id being that they are the join table and belong to both. They also have fields to input their name and age. The user table has fields for their name, email, password_digest(which holds their password encrypted), and a uid field for holding their random password generated with SecureRandom.hex in creating their account through logging in through facebook.   
  The team and players have full CRUD (Create, Read, Update, Delete) functionality instatiated through their controllers.  The user/coaches have functionality to create, read through their controller. The sessions controller handles logging in through my site or optionally through Facebook using the Omniauth gem.  The bcrypt gem was also used to handle having a secure password and authentication. I used to basic validations for models of fields have to be present and email being unique, to verify before saving to the database everything is filled in and there aren’t duplicates.  
In creating the views I implemented partials for the main form for a team and player to be rendered in both the new and edit files.  Both models also containing index and show folders to be able to read all teams/players, or individual team/player. The user views contain just index, new, and show. While the sessions holds the views for the main home page and login page. Every form view page also contains code to display the validation errors when page reloads without saving. 
		<% if @team.errors.any? %> 
        		<div id= "error_explanation"> 
            <ul>
                <% @team.errors.full_messages do |message| %> 
                    <li><%= message %></li>
                <% end %>
            </ul> 
        </div>
    <% end %> 


Making my routes I used basic get/post routes for handling my signup/login/logout actions.  Resources used for all models, to be have availability to all their conrtroller actions. Nested resources used for a user to team, to be able in instatiate a team to a user and offer a user/1/team/new helper route. As well as a team to a user to then be able to instatiate a player to a team and offer a teams/1/players/new helper routes.  

		root 'sessions#home' 

  get '/createaccount' => "users#new"
  get '/login' => "sessions#new" 
  get '/auth/facebook/callback' => 'sessions#fbcreate' 
  post '/login' => "sessions#create" 
  get '/logout' => "sessions#destroy" 

  resources 'users'
  resources 'teams'
  resources 'players'

  post 'teams/new' => "teams#new"
  post 'players/new' => "players#new"  

  resources :users, only: [:show, :index] do 
    resources :teams, only: [:show, :index, :new] 
  end 

  resources :teams do 
    resources :players, only: [:index, :new] 
  end 


 

