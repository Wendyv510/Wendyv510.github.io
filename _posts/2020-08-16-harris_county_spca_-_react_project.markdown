---
layout: post
title:      " Harris County SPCA - React Project "
date:       2020-08-16 20:11:02 +0000
permalink:  harris_county_spca_-_react_project
---


For the final module in the Flatiron School Software Engineering program, we learned React + Redux. For my project I chose to make a mock SPCA site, Harris County SPCA.  I started with putting together a backend API with Rails. Cats, dogs, and applicants as my models, having controllers with index, create, show, destroy capabilities.  CORS(Cross-origin resource sharing) was implemented in my Gemfile, to allow the frontend to fetch the data stored in the Rails API backend.  As well as the Fast JSON API  gem, to generate serializer classes for each resource object being passed to the frontend.
The frontend and backend I set up as separate repositories, frontend at https://github.com/Wendyv510/harris-county-spca-frontend, and the backend at https://github.com/Wendyv510/HarrisCountySPCA-backend.
For the backend I used the node module create-react-app, to generate a boilerplate version of a React application.  From there I used the yarn command(similar to npm) to add react-redux, redux-thunk, and react-router-dom packages to my package.json file.  Then running yarn install for all my packages, then yarn start to open in the browser at http://localhost:3000.  Using the router I set my routes through their components to home, cats, dogs, apply, with applicants also being an option, but not having a link button, further would implement a administrator sign in to be able to access the applicants information.  
<Router>
        <Navbar/>
          <Switch>
            <Route exact path="/" component = {Home}/>
            <Route exact path="/cats" component = {CatsContainer}/>
            <Route exact path="/dogs" component = {DogsContainer}/>
            <Route exact path="/applicants" component = {ApplicantsContainer}/>
            <Route exact path="/apply" component = {ApplicantForm}/>
            <Redirect from= "/apply" to= '/'/>
          </Switch>
      </Router>

A catReducer, dogReducer, and applicantReducer were implemented to set original state.  Then would use the switch element to take in and handle the action components such as ‘FETCH_CATS’ as well as dogs and applicants, with applicants also have an ‘ADD_APPLICATANT’ action.  Container components were set up as the parent components where the fetch actions are called in the componentDidMount.  Then in the return are passing down props to the child components, and utilizing the reducers in the mapStateToProps function and then connecting to the redux store.  
import React, {Component} from 'react'
import fetchCats from '../actions/fetchCats'
import Cats from '../components/Cats' 
import { connect } from 'react-redux'

class CatsContainer extends Component {
    
    componentDidMount(){
         this.props.fetchCats()
    }
    

    render(){
        
        return(
            <div className="cats">
                <Cats felines = {this.props.cats}/>
            </div>
        )
    }
}

const mapStateToProps = (state) => {
    return{
        cats: state.catReducer.cats
    }
}

export default connect(mapStateToProps, {fetchCats})(CatsContainer) 

In the index.js file I implemented middleware thunk and createStore from redux. As well as combineReducer to put all the reducer into one rootReducer to user then in the create store for the data of each component.  One form was used in the application to allow users to apply to adopt and animal.  Within the ApplicantForm.js file handleOnchange and handleSubmit were implemented to handle events, and get the values input from the form and setState with the data.  

