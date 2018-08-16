---
layout: post
title:  "High order components with react"
date:   2017-05-07 12:13:23 +0200
categories: reactjs update
hero: "assets/img/react.png"
overlay: blue
---
High order component (HOC) is a technique in react for reusing component logic.
HOCs are not part of the React API.
They are a pattern that emerges from react’s compositional nature.
{: .lead}
<!–-break-–>
a HOC function takes a component and returns a new component


Whereas a component transforms props into UI a HOC transforms a component into another component.

A High Order Component is a pure function with zero side effects

Why High order components are useful.

Components are a unit of reuse in react  but some patterns of component reuse are not straightforward.
suppose we have two components that should only get displayed when authentication is successful.

~~~ javascript
import React, {Component} from 'react'
import Auth from '../utils/AuthService'
import DashboardDetails from '../components/layout'

const Auth = new AuthService();
class Dashboard extends Component {

   constructor(props){
     super(props)
     this.state = {
     isLoading: true
   }
 }
   componentDidMount(){
     if(!Auth.loggedIn()){
        Router.push('/')
    }else{
        this.setState = {isLoading: false}
     }
   }

   render(){
     return !this.state.isLoading?
            <DashboardDetails details={Auth.getDashboardDetails}/> :
            <div> loading ...</div>
   }
}

export default Dashboard
~~~

Then add the second component which follows a similar pattern which requires authentication and displays loading while authentication is not comfirmed.

~~~ javascript
import React, {Component} from 'react'
import Auth from '../utils/AuthService'
import ProfileDetails from '../components/ProfileDetails'

const Auth = new AuthService();
class Profile extends Component {

   constructor(props){
       super(props)
       this.state = {
       isLoading: true
     }
   }
    componentDidMount(){
      if(!Auth.loggedIn()){
        Router.push('/')
       } else{ this.setState = {isLoading: false}
     }
   }

   render(){
      return !this.state.isLoading?
      <ProfileDetails profile={Auth.getProfile} :
      <div> loading ...</div>
   }
}

export default Profile

~~~

Though the two components Profile and Dashboard  are not identical much of their implementation is similar.
on componentDidMount we check whether a user is loggedIn. If the user is logged in,  isLoading is set to false and if not the user gets redirected to the home page.

When the application grows this pattern can lead to a lot of duplication. We need to abstract the logic in one place and share it across components.
This is where high order components become useful. We can write a high order component that receives a child component which requires authentication as one of its arguments.

~~~ ruby

import React, {Component} from 'react'
import AuthService from '.utils/AuthService'
import Router from 'next/router'

export default function withAuth(AuthComponent){
const Auth = new AuthService();
    return class Authenticated extends Component{
        constructor(props){
            super(props)
            this.state = {
                isLoading: true
            }
        }
        componentDidMount(){
            if (!Auth.loggedIn()) {
                Router.push('/')
            }
            this.setState({isLoading: false})
        }
        render(){
            return (
                <div>
                    {this.state.isLoading ? <div>Loading ... </div> :
                       <AuthComponent {...this.props} auth={Auth} />}
                </div>
            )
        }
    }
}
~~~

The HOC does not modify the component nor does it use inheritance to copy its behaviour. It is a pure function without side effects that wraps the original component in a container component. The original component will receive props from the container component which it will use to render its output.
The HOC should not mutate the components props in any way.

The dashboard component would be changed to :

~~~ ruby
import React, {Component} from 'react'
import DashboardDetails from '../components/layout'
import withAuth from '../components/withAuth'

class Dashboard extends Component {
  render(){
    const details = this.props.auth.getDashboardDetails()
    return  <DashboardDetails details={details} />
   }
}

export default withAuth(Dashboard)
~~~

The profile component would be changed to :

~~~ ruby
import React, {Component} from 'react'
import DashboardDetails from '../components/layout'
import withAuth from '../components/withAuth'

class Profile extends Component {
   render(){
    const profile = this.props.auth.getProfile()
    return  <ProfileDetails profile={profile} />
   }
}

export default withAuth(Profile)
~~~

This pattern is much more flexible and enables us to change how we handle authentication in one place.
