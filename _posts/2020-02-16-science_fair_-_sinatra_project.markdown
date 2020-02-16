---
layout: post
title:      "Science Fair - Sinatra Project "
date:       2020-02-16 21:38:12 +0000
permalink:  science_fair_-_sinatra_project
---


	In Flatiron Software Engineering program, a Ruby Sinatra project is the second main program you’re expected to build on your own. Sinatra being our mode of Web Application Framework we’re using. Implementing the gem corneal within, which sets up your main framework and functionalities. Then using the MVC (Model, Views, Controllers) to configure the app you’re developing.
 My Sinatra project is a high school science fair application.  The welcome page has a greeting and an option to sign up, or sign in.  My two models corresponding are teachers(being the user) that will be the ones interacting with the app, and their students of whom they’ll be enrolling in the science fair. Being that teachers  ‘have_many’ students, and students ‘belong_to’ a teacher.  In the views category, I have two folders users, and students. With users starting with a form to sign up, where they will be asked their name, email, and password.  Which then redirects to a sign in page, needing just the email and password.  If entered correctly then sends them to a greeting page with button options to either view all their students, enroll or edit students, or log out.  If not entered correctly redirects them to a sign in failure page, prompting them to sign up first, or review email/password and try again.  			In the students view folder, there is an index file, that the teachers are directed to when choosing the view students button. There is an new file, that contains the form to enroll a new student by inputting their name, grade level, and project title.  Then there is a show file which shows the student/info you just submitted in the new form, as well as button options to edit or delete.  On all the pages it also gives the user/teacher the option to view all, or log out.  
There are three main controllers implemented to function the application, overall app controller, responsible to initialize opening welcome page.  Then a user controller getting and posting initial sign up and sign in data. Then a student controller that contains all the CRUD (create, read, update, delete) actions for carrying out the different needs of the user throughout use of the application using Sinatra RESTful routes for mapping HTTP verb requests. 
There were a few main concept requirements to input within the user interface. One being to ensure input validations upon signing in, so their email and password must be correct when trying to access.   In the user_controller.rb file implemented as follows within the post ‘/signin’ action. 
post "/signin" do 
    @user = User.find_by(:email => params[:email]) 
       if @user && @user.authenticate(params[:password])
        session[:user_id] = @user.id 
          erb :'/user/show'
      else 
          redirect to '/user/failure' 
      end 
  end
With them then being redirected to a failure page if not correct. In the views/user folder, as an erb file.  They’ll see in their browser of a new page, redirected to. 
*** Sign In Failure ***
Email and/or password invalid
If you don't already have an existing account, please Sign Up
Or verify email & password and try again Sign In

As well as user authentication put in place as safe fails, on the sign up, sign in, and enrolling new students pages, it is programmed that the fields are required.  So they must input data to move on, verifying no black data passed through to the databases.  
Another key concept in user data input applications, is ensuring only the user can edit or delete their information.  Implemented in the student_controller.rb file, within the get ‘/students/:id/edit’ action, verifying that the student is one of the current_users students. If they aren’t one of the users students, then being redirected back to the main student index page.  In going further and doing more with this application, I would have a flash message here, saying you can only edit/delete your own students. 

get '/students/:id/edit' do
    if @student = User.current_user(session).students.find_by_id(params[:id]) 
       erb :'/students/show'
    else 
      redirect to "/students" 
    end
The content of your blog post goes here.
