---
title: Personal Project Management-Frontend(1)
subtitle: '"“Only the paranoid survive.” — Andy Grove"'
date: 2020-03-29 20:09:12
tags:
---

![image](https://miro.medium.com/max/1400/0*eDuuXtQKVoYqCMh3)

> Demonstrating computational thinking or the ability to break down large, complex problems is just as valuable (if not more so) than the baseline technical skills required for a job.” — Hacker Rank (2018 Developer Skills Report)

Content:

<!-- TOC -->

- [Create React App](#create-react-app)
  - [Start Application](#start-application)
- [First Reacct Component](#first-reacct-component)
  - [Project and Header Components](#project-and-header-components)
  - [Bringing BootStrap 4](#bringing-bootstrap-4)
  - [Style out Dashboard, Navibar, ProjectItem](#style-out-dashboard-navibar-projectitem)
  - [React Router, first Functional Component](#react-router-first-functional-component)

<!-- /TOC -->

## Create React App

Under the Folder PPMToolFullStack:
**Terminal:**

```shell script
npm install -g create-react-app
cd "folder name"
create-react-app "folder name"
```

### Start Application

```shell script
npm start
```

## First Reacct Component

1. Create n new folder **components** under src
2. Create the first JS file named **Dashboard**
3. Using "**rrc**" shortcut to create Dashboard component

```javascript
import React, { Component } from "react";

export default class Dashboard extends Component {
  render() {
    return <h1>Welcome to the Dashboard</h1>;
  }
}
```

4. Import Dashboard component using the following syntax in App.js

```javascript
import React from "react";
import "./App.css";
import Dashboard from "./components/Dashboard";

function App() {
  return (
    <div className="App">
      <Dashboard />
    </div>
  );
}

export default App;
```

5. Start the Application using:

```shell script
npm start
```

### Project and Header Components

1. Create ProjectItem.js under Project folder

```javascript
import React, { Component } from "react";

export default class ProjectItem extends Component {
  render() {
    return (
      <div>
        <h1>ProjectItem</h1>
      </div>
    );
  }
}
```

2. Import ProjectItem Component in Dashboard

```javascript
import React, { Component } from "react";
import ProjectItem from "./Project/ProjectItem";

export default class Dashboard extends Component {
  render() {
    return (
      <div>
        <h1>Welcome to the Dashboard</h1>
        <ProjectItem />
      </div>
    );
  }
}
```

3. npm start:
   ![result1](result1.png)

4. Create Header.js under Layout

```javascript
import React, { Component } from "react";

export default class Header extends Component {
  render() {
    return (
      <div>
        <h1>Navibar</h1>
      </div>
    );
  }
}
```

5. Import Header component in App.js

```javascript
import React from "react";
import "./App.css";
import Dashboard from "./components/Dashboard";
import Header from "./components/Layout/Header";

function App() {
  return (
    <div className="App">
      <Header />
      <Dashboard />
    </div>
  );
}

export default App;
```

6. npm start

![Navibar](Navibar.png)

### Bringing BootStrap 4

1. Install bootstrap

```shell script
hewenyong@nanbunyuus-MacBook-puro ppmtool-react-client % npm install bootstrap
```

2. Import css from bootstrap in App.js

```javascript
import "bootstrap/dist/css/bootstrap.min.css";
```

3. Test bootstrap in Dashboard

```javascript
import React, { Component } from "react";
import ProjectItem from "./Project/ProjectItem";

export default class Dashboard extends Component {
  render() {
    return (
      <div>
        <h1 className="alert alert-warning">Welcome to the Dashboard</h1>
        <ProjectItem />
      </div>
    );
  }
}
```

4. Result
   ![result7](result7.png)

### Style out Dashboard, Navibar, ProjectItem

1. Finish Header.js

```javascript
import React, { Component } from "react";

export default class Header extends Component {
  render() {
    return (
      <nav className="navbar navbar-expand-sm navbar-dark bg-primary mb-4">
        <div className="container">
          <a className="navbar-brand" href="Dashboard.html">
            Personal Project Management Tool
          </a>
          <button
            className="navbar-toggler"
            type="button"
            data-toggle="collapse"
            data-target="#mobile-nav"
          >
            <span className="navbar-toggler-icon" />
          </button>

          <div className="collapse navbar-collapse" id="mobile-nav">
            <ul className="navbar-nav mr-auto">
              <li className="nav-item">
                <a className="nav-link" href="/dashboard">
                  Dashboard
                </a>
              </li>
            </ul>

            <ul className="navbar-nav ml-auto">
              <li className="nav-item">
                <a className="nav-link " href="register.html">
                  Sign Up
                </a>
              </li>
              <li className="nav-item">
                <a className="nav-link" href="login.html">
                  Login
                </a>
              </li>
            </ul>
          </div>
        </div>
      </nav>
    );
  }
}
```

2. Finish Dashboard.js

```javascript
import React, { Component } from "react";
import ProjectItem from "./Project/ProjectItem";

export default class Dashboard extends Component {
  render() {
    return (
      <div className="projects">
        <div className="container">
          <div className="row">
            <div className="col-md-12">
              <h1 className="display-4 text-center">Projects</h1>
              <br />
              <a href="ProjectForm.html" className="btn btn-lg btn-info">
                Create a Project
              </a>
              <br />
              <hr />
              {/* Project Item Component */}
              <ProjectItem />
              {/* End of Project Item Component */}
            </div>
          </div>
        </div>
      </div>
    );
  }
}
```

3. Finish ProjectItem.js

```js
import React, { Component } from "react";

export default class ProjectItem extends Component {
  render() {
    return (
      <div className="container">
        <div className="card card-body bg-light mb-3">
          <div className="row">
            <div className="col-2">
              <span className="mx-auto">REACT</span>
            </div>
            <div className="col-lg-6 col-md-4 col-8">
              <h3>Spring / React Project</h3>
              <p>Project to create a Kanban Board with Spring Boot and React</p>
            </div>
            <div className="col-md-4 d-none d-lg-block">
              <ul className="list-group">
                <a href="#">
                  <li className="list-group-item board">
                    <i className="fa fa-flag-checkered pr-1"> Project Board </i>
                  </li>
                </a>
                <a href="#">
                  <li className="list-group-item update">
                    <i className="fa fa-edit pr-1"> Update Project Info</i>
                  </li>
                </a>
                <a href="">
                  <li className="list-group-item delete">
                    <i className="fa fa-minus-circle pr-1"> Delete Project</i>
                  </li>
                </a>
              </ul>
            </div>
          </div>
        </div>
      </div>
    );
  }
}
```

4. Add <Link /> Tag in Index.html

```html
<link
  rel="stylesheet"
  href="https://use.fontawesome.com/releases/v5.2.0/css/all.css"
  integrity="sha384-hWVjflwFxL6sNzntih27bfxkr27PmbbK/iSvJ+a4+0owXq79v+lsFkW54bOGbiDQ"
  crossorigin="anonymous"
/>
```

5. Result
   ![day4](day4.png)

### React Router, first Functional Component

1. Install react-router-dom

```shell script
npm install react-router-dom
```

2. Import "react-router-dom" in App.js

```javascript
import React from 'react';
import './App.css';
import Dashboard from './components/Dashboard';
import Header from './components/Layout/Header';
import "bootstrap/dist/css/bootstrap.min.css";
import { BrowserRouter as Router, Route} from "react-router-dom";
import AddProject from './components/Project/AddProject';
function App() {
  return (
    <Router>
      <div className="App">
        <Header />
        {/* <Dashboard /> */}
        <Route exact path="/addProject" component={AddProject}/>
        <Route exact path="/dashboard" component={Dashboard}/>
      </div>
    </Router>
    
  );
}

export default App;

export default App;
```

3. Create CreateProjectButton.js

```javascript
import React from "react";
import { Link } from "react-router-dom";
const CreateProjectButton = () => {
  return (
    <React.Fragment>
      <Link to="/addProject" className="btn btn-lg btn-info">
        Create a Project
      </Link>
    </React.Fragment>
  );
};

export default CreateProjectButton;
```

4. Dashboard.js

```javascript
import React, { Component } from "react";
import ProjectItem from "./Project/ProjectItem";
import CreateProjectButton from "./Project/CreateProjectButton";

export default class Dashboard extends Component {
  render() {
    return (
      <div className="projects">
        <div className="container">
          <div className="row">
            <div className="col-md-12">
              <h1 className="display-4 text-center">Projects</h1>
              <br />
              <CreateProjectButton />
              <br />
              <hr />
              {/* Project Item Component */}
              <ProjectItem />
              {/* End of Project Item Component */}
            </div>
          </div>
        </div>
      </div>
    );
  }
}
```

5. Click `Create a Project`, magic happened.
   ![day4](day4-2.png)

### AddProject Component - controlled form

````javascript
import React, { Component } from "react";

class AddProject extends Component {
  constructor() {
    super();

    this.state = {
      projectName: "",
      projectIdentifier: "",
      description: "",
      start_date: "",
      end_date: ""
    };

    this.onChange = this.onChange.bind(this);
    this.onSubmit = this.onSubmit.bind(this);
  }

  onChange(e) {
    this.setState({ [e.target.name]: e.target.value });
  }

  onSubmit(e) {
    e.preventDefault();
    const newProject = {
      projectName: this.state.projectName,
      projectIdentifier: this.state.projectIdentifier,
      description: this.state.description,
      start_date: this.state.start_date,
      end_date: this.state.end_date
    };

    console.log(newProject);
  }

  render() {
    return (
      <div>
        {
          //check name attribute input fields
          //create constructor
          //set state
          //set value on input fields
          //create onChange function
          //set onChange on each input field
          //bind on constructor
          //check state change in the react extension
        }

        <div className="project">
          <div className="container">
            <div className="row">
              <div className="col-md-8 m-auto">
                <h5 className="display-4 text-center">Create Project form</h5>
                <hr />
                <form onSubmit={this.onSubmit}>
                  <div className="form-group">
                    <input
                      type="text"
                      className="form-control form-control-lg "
                      placeholder="Project Name"
                      name="projectName"
                      value={this.state.projectName}
                      onChange={this.onChange}
                    />
                  </div>
                  <div className="form-group">
                    <input
                      type="text"
                      className="form-control form-control-lg"
                      placeholder="Unique Project ID"
                      name="projectIdentifier"
                      value={this.state.projectIdentifier}
                      onChange={this.onChange}
                    />
                  </div>
                  <div className="form-group">
                    <textarea
                      className="form-control form-control-lg"
                      placeholder="Project Description"
                      name="description"
                      value={this.state.description}
                      onChange={this.onChange}
                    />
                  </div>
                  <h6>Start Date</h6>
                  <div className="form-group">
                    <input
                      type="date"
                      className="form-control form-control-lg"
                      name="start_date"
                      value={this.state.start_date}
                      onChange={this.onChange}
                    />
                  </div>
                  <h6>Estimated End Date</h6>
                  <div className="form-group">
                    <input
                      type="date"
                      className="form-control form-control-lg"
                      name="end_date"
                      value={this.state.end_date}
                      onChange={this.onChange}
                    />
                  </div>

                  <input
                    type="submit"
                    className="btn btn-primary btn-block mt-4"
                  />
                </form>
              </div>
            </div>
          </div>
        </div>
      </div>
    );
  }
}

export default AddProject;
````
## Create Redux Store
 <img id="May3_6" src="May3_6.png">
<style>
#May3_6 {
   border: 2px solid #ddd;
   display: inline-block;
}
</style>
1. Install Redux
```shell script
npm i redux react-redux redux-thunk
```
2. Install axios
```shell script
npm i axios
```
3. `App.js`
```javascript
import React from 'react';
import './App.css';
import Dashboard from './components/Dashboard';
import Header from './components/Layout/Header';
import "bootstrap/dist/css/bootstrap.min.css";
import { BrowserRouter as Router, Route} from "react-router-dom";
import AddProject from './components/Project/AddProject';
import { Provider } from 'react-redux'
import store from './store'

function App() {
  return (
    <Provider store={store}>
      <Router>
      <div className="App">
        <Header />
        {/* <Dashboard /> */}
        <Route exact path="/addProject" component={AddProject}/>
        <Route exact path="/dashboard" component={Dashboard}/>
      </div>
      </Router>
    </Provider>
    
    
  );
}

export default App;

```
4. `reducer.js`
```javascript
import {combineReducers} from 'redux'

export default combineReducers ({
    
})
```
5. `store.js`
```javascript
import {createStore, applyMiddleware, compose} from 'redux'
import thunk from 'redux-thunk'
import rootReducer from './reducers'


const initalState = {};
const middleware = [thunk];

let store 

if (window.navigator.userAgent.includes("Chrome")) {
    store = createStore(
        rootReducer,
        initalState,
        compose(
            applyMiddleware(...middleware),
            window.__REDUX_DEVTOOLS_EXTENSION__ && 
            window.__REDUX_DEVTOOLS_EXTENSION__()
        )
    );
} else {
    store = createStore(
        rootReducer,
        initalState,
        compose(
            applyMiddleware(...middleware)
        )
    );
}
export default store;
```
6. Structure
<img id="day11" src="day11.png" >

<style>
#day11 {
    width: 40%;
    height: 40%;
    border: 1px solid #ddd;
    display: inline-block;
}
</style>

## Create Project from React
1. `projectAction.js`
```javascript
import axios from "axios"
import { GET_ERRORS } from "./types"

export const createProject = (project, history) => async dispatch => {
    try {
        const res = await axios.post("http://localhost:8080/api/project", project);
        history.push("/dashboard")
    } catch (err) {
        dispatch({
            type:GET_ERRORS,
            payload:err.response.data
        })
    }
}
```
2. `types.js`
```javascript
export const GET_ERRORS = "GET_ERRORS"
```
3. `errorReducer.js`
```javascript
import {GET_ERRORS} from "../actions/types"

const initialState = {};

export default function(state = initialState, action) {
    switch (action.type) {
        case GET_ERRORS:
            return action.payload;
        default:
            return state
    }
}
```
4. Run Java server
5. Run `npm start`
6. Result in H2
<img src="May3.png">

## Get Validation errors from Redux
1. If we submit with blanks, there would be errors showing in state
<img src="May3_2.png">
2. `AddProject.js`
```javascript
import React, { Component } from "react";
import PropTypes from "prop-types"
import { connect } from "react-redux"
import { createProject } from "../../actions/projectActions"

class AddProject extends Component {
  constructor() {
    super();

    this.state = {
      projectName: "",
      projectIdentifier: "",
      description: "",
      start_date: "",
      end_date: "",
      errors: {}
    };

    this.onChange = this.onChange.bind(this);
    this.onSubmit = this.onSubmit.bind(this);
  }

  //life cycle hooks
  componentWillReceiveProps(nextProps) {
    if (nextProps.errors) {
      this.setState({errors: nextProps.errors})
    }
  }

  onChange(e) {
    this.setState({ [e.target.name]: e.target.value });
  }

  onSubmit(e) {
    e.preventDefault();
    const newProject = {
      projectName: this.state.projectName,
      projectIdentifier: this.state.projectIdentifier,
      description: this.state.description,
      start_date: this.state.start_date,
      end_date: this.state.end_date
    };
    this.props.createProject(newProject, this.props.history)
  }

  render() {
    const { errors } = this.state

    return (
      <div>
        <div className="project">
          <div className="container">
            <div className="row">
              <div className="col-md-8 m-auto">
                <h5 className="display-4 text-center">Create Project form</h5>
                <hr />
                <form onSubmit={this.onSubmit}>
                  <div className="form-group">
                    <input
                      type="text"
                      className="form-control form-control-lg "
                      placeholder="Project Name"
                      name="projectName"
                      value={this.state.projectName}
                      onChange={this.onChange}
                    />
                    {/* <p>{errors.projectName}</p> */}
                  </div>
                  <div className="form-group">
                    <input
                      type="text"
                      className="form-control form-control-lg"
                      placeholder="Unique Project ID"
                      name="projectIdentifier"
                      value={this.state.projectIdentifier}
                      onChange={this.onChange}
                    />
                  </div>
                  <div className="form-group">
                    <textarea
                      className="form-control form-control-lg"
                      placeholder="Project Description"
                      name="description"
                      value={this.state.description}
                      onChange={this.onChange}
                    />
                  </div>
                  <h6>Start Date</h6>
                  <div className="form-group">
                    <input
                      type="date"
                      className="form-control form-control-lg"
                      name="start_date"
                      value={this.state.start_date}
                      onChange={this.onChange}
                    />
                  </div>
                  <h6>Estimated End Date</h6>
                  <div className="form-group">
                    <input
                      type="date"
                      className="form-control form-control-lg"
                      name="end_date"
                      value={this.state.end_date}
                      onChange={this.onChange}
                    />
                  </div>

                  <input
                    type="submit"
                    className="btn btn-primary btn-block mt-4"
                  />
                </form>
              </div>
            </div>
          </div>
        </div>
      </div>
    );
  }
}

AddProject.propTypes = {
  createProject : PropTypes.func.isRequired,
  errors: PropTypes.object.isRequired
}

const mapStateToProps = state => ({
  errors: state.errors
})

export default connect(mapStateToProps, { createProject })(AddProject);
```
3. Result
<img id="May3_3" src="May3_3.png">
<style>
#May3_3 {
    border: 1px solid #ddd;
    display: inline-block;
}
</style>

4. `AddProject.js`
```javascript
import React, { Component } from "react";
import PropTypes from "prop-types"
import { connect } from "react-redux"
import { createProject } from "../../actions/projectActions"

class AddProject extends Component {
  constructor() {
    super();

    this.state = {
      projectName: "",
      projectIdentifier: "",
      description: "",
      start_date: "",
      end_date: "",
      errors: {}
    };

    this.onChange = this.onChange.bind(this);
    this.onSubmit = this.onSubmit.bind(this);
  }

  //life cycle hooks
  componentWillReceiveProps(nextProps) {
    if (nextProps.errors) {
      this.setState({errors: nextProps.errors})
    }
  }

  onChange(e) {
    this.setState({ [e.target.name]: e.target.value });
  }

  onSubmit(e) {
    e.preventDefault();
    const newProject = {
      projectName: this.state.projectName,
      projectIdentifier: this.state.projectIdentifier,
      description: this.state.description,
      start_date: this.state.start_date,
      end_date: this.state.end_date
    };
    this.props.createProject(newProject, this.props.history)
  }

  render() {
    const { errors } = this.state

    return (
      <div>
        <div className="project">
          <div className="container">
            <div className="row">
              <div className="col-md-8 m-auto">
                <h5 className="display-4 text-center">Create Project form</h5>
                <hr />
                <form onSubmit={this.onSubmit}>
                  <div className="form-group">
                    <input
                      type="text"
                      className="form-control form-control-lg "
                      placeholder="Project Name"
                      name="projectName"
                      value={this.state.projectName}
                      onChange={this.onChange}
                    />
                    <p style={{color:'red'}}>{errors.projectName}</p>
                  </div>
                  <div className="form-group">
                    <input
                      type="text"
                      className="form-control form-control-lg"
                      placeholder="Unique Project ID"
                      name="projectIdentifier"
                      value={this.state.projectIdentifier}
                      onChange={this.onChange}
                    />
                     <p style={{color:'red'}}>{errors.projectIdentifier}</p>
                  </div>
                  <div className="form-group">
                    <textarea
                      className="form-control form-control-lg"
                      placeholder="Project Description"
                      name="description"
                      value={this.state.description}
                      onChange={this.onChange}
                    />
                     <p style={{color:'red'}}>{errors.description}</p>
                  </div>
                  <h6>Start Date</h6>
                  <div className="form-group">
                    <input
                      type="date"
                      className="form-control form-control-lg"
                      name="start_date"
                      value={this.state.start_date}
                      onChange={this.onChange}
                    />
                  </div>
                  <h6>Estimated End Date</h6>
                  <div className="form-group">
                    <input
                      type="date"
                      className="form-control form-control-lg"
                      name="end_date"
                      value={this.state.end_date}
                      onChange={this.onChange}
                    />
                  </div>

                  <input
                    type="submit"
                    className="btn btn-primary btn-block mt-4"
                  />
                </form>
              </div>
            </div>
          </div>
        </div>
      </div>
    );
  }
}

AddProject.propTypes = {
  createProject : PropTypes.func.isRequired,
  errors: PropTypes.object.isRequired
}

const mapStateToProps = state => ({
  errors: state.errors
})

export default connect(mapStateToProps, { createProject })(AddProject);
```
5. Update Result
   <img id="May3_4" src="May3_4.png">
   <style>
   #May3_4 {
       border: 1px solid #ddd;
       display: inline-block;
   }
   </style>

6. Test: Creating Same Project for Two Times
   <img id="May3_5" src="May3_5.png">
   <style>
   #May3_5 {
       border: 2px solid #ddd;
       display: inline-block;
   }
   </style>


## Style Validation errors with Classnames
1. Install classnames
```shell script
npm i classnames
```
2. `AddProject.js`
```javascript
import React, { Component } from "react";
import PropTypes from "prop-types"
import { connect } from "react-redux"
import { createProject } from "../../actions/projectActions"
import classnames from "classnames"

class AddProject extends Component {
  constructor() {
    super();

    this.state = {
      projectName: "",
      projectIdentifier: "",
      description: "",
      start_date: "",
      end_date: "",
      errors: {}
    };

    this.onChange = this.onChange.bind(this);
    this.onSubmit = this.onSubmit.bind(this);
  }

  //life cycle hooks
  componentWillReceiveProps(nextProps) {
    if (nextProps.errors) {
      this.setState({errors: nextProps.errors})
    }
  }

  onChange(e) {
    this.setState({ [e.target.name]: e.target.value });
  }

  onSubmit(e) {
    e.preventDefault();
    const newProject = {
      projectName: this.state.projectName,
      projectIdentifier: this.state.projectIdentifier,
      description: this.state.description,
      start_date: this.state.start_date,
      end_date: this.state.end_date
    };
    this.props.createProject(newProject, this.props.history)
  }

  render() {
    const { errors } = this.state

    return (
      <div>
        <div className="project">
          <div className="container">
            <div className="row">
              <div className="col-md-8 m-auto">
                <h5 className="display-4 text-center">Create Project form</h5>
                <hr />
                <form onSubmit={this.onSubmit}>
                  <div className="form-group">
                    <input
                      type="text"
                      className={classnames("form-control form-control-lg", {"is-invalid": errors.projectName})}
                      placeholder="Project Name"
                      name="projectName"
                      value={this.state.projectName}
                      onChange={this.onChange}
                    />
                    {errors.projectName && (<div className="invalid-feedback">{errors.projectName}</div>)}
                  </div>
                  <div className="form-group">
                    <input
                      type="text"
                      className={classnames("form-control form-control-lg", {"is-invalid": errors.projectIdentifier})}
                      placeholder="Unique Project ID"
                      name="projectIdentifier"
                      value={this.state.projectIdentifier}
                      onChange={this.onChange}
                    />
                     {errors.projectIdentifier && (<div className="invalid-feedback">{errors.projectIdentifier}</div>)}
                  </div>
                  <div className="form-group">
                    <textarea
                      className={classnames("form-control form-control-lg", {"is-invalid": errors.description})}
                      placeholder="Project Description"
                      name="description"
                      value={this.state.description}
                      onChange={this.onChange}
                    />
                     {errors.description && (<div className="invalid-feedback">{errors.description}</div>)}
                  </div>
                  <h6>Start Date</h6>
                  <div className="form-group">
                    <input
                      type="date"
                      className="form-control form-control-lg"
                      name="start_date"
                      value={this.state.start_date}
                      onChange={this.onChange}
                    />
                  </div>
                  <h6>Estimated End Date</h6>
                  <div className="form-group">
                    <input
                      type="date"
                      className="form-control form-control-lg"
                      name="end_date"
                      value={this.state.end_date}
                      onChange={this.onChange}
                    />
                  </div>

                  <input
                    type="submit"
                    className="btn btn-primary btn-block mt-4"
                  />
                </form>
              </div>
            </div>
          </div>
        </div>
      </div>
    );
  }
}

AddProject.propTypes = {
  createProject : PropTypes.func.isRequired,
  errors: PropTypes.object.isRequired
}

const mapStateToProps = state => ({
  errors: state.errors
})

export default connect(mapStateToProps, { createProject })(AddProject);
```
3. Result
<img id="May6_1" src="May6_1.png">
   <style>
   #May6_1 {
       border: 1px solid #ddd;
       display: inline-block;
   }
   </style>

## Get Project - Redux Only
1. Create `projectReducer.js` in reducers folder
```javascript
import { GET_PROJECTS } from "../actions/types"

const initialState = {
    projects: [],
    project: {}
}

export default function (state = initialState, action) {
    switch (action.type) {
        case GET_PROJECTS:
            return {
                ...state,
                projects: action.payload
            }
    
        default:
            return state;
    }
}
```
2. `index.js`
```javascript
import {combineReducers} from 'redux'
import errorReducer from "./errorReducer"
import projectReducer from './projectReducer'

export default combineReducers ({
    errors: errorReducer,
    project: projectReducer
})
```
3. `projectActions.js`
```javascript
import axios from "axios"
import { GET_ERRORS, GET_PROJECTS} from "./types"

export const createProject = (project, history) => async dispatch => {
    try {
        const res = await axios.post("http://localhost:8080/api/project", project);
        history.push("/dashboard")
    } catch (err) {
        dispatch({
            type:GET_ERRORS,
            payload:err.response.data
        })
    }
}

export const getProjects = () => async dispatch => {
    const res = await axios.get("http://localhost:8080/api/project/all")
    dispatch ({
        type: GET_PROJECTS,
        payload: res.data
    })
}
```

4. `Dashboard.js`
```javascript
import React, { Component } from 'react'
import ProjectItem from './Project/ProjectItem'
import CreateProjectButton from './Project/CreateProjectButton';
import { connect } from "react-redux"
import { getProjects } from "../actions/projectActions"
import PropTypes from "prop-types"

class Dashboard extends Component {

    componentDidMount() {
        this.props.getProjects()
    }

    render() {
        return (
            <div className="projects">
        <div className="container">
            <div className="row">
                <div className="col-md-12">
                    <h1 className="display-4 text-center">Projects</h1>
                    <br />
                    <CreateProjectButton />
                    <br />
                    <hr />
                    {/* Project Item Component */}
                    <ProjectItem />
                    {/* End of Project Item Component */}
                </div>
            </div>
        </div>
    </div>
            
        );
    }
}

Dashboard.propTypes= {
    project: PropTypes.object.isRequired,
    getProjects: PropTypes.func.isRequired
}

const mapStateToProps = state => ({
    project: state.project

})
export default connect(mapStateToProps, {getProjects })(Dashboard)

```
5. Result
<img src="May6_2.png">

## Get Project-Final Step
1. `Dashboard.js`
```javascript
import React, { Component } from 'react'
import ProjectItem from './Project/ProjectItem'
import CreateProjectButton from './Project/CreateProjectButton';
import { connect } from "react-redux"
import { getProjects } from "../actions/projectActions"
import PropTypes from "prop-types"

class Dashboard extends Component {

    componentDidMount() {
        this.props.getProjects()
    }

    render() {

        const {projects} = this.props.project

        return (
            <div className="projects">
        <div className="container">
            <div className="row">
                <div className="col-md-12">
                    <h1 className="display-4 text-center">Projects</h1>
                    <br />
                    <CreateProjectButton />
                    <br />
                    <hr />
                    {/* Project Item Component */}
                    {projects.map(project=>(
                        <ProjectItem key={project.id} project={project}/>
                    ))

                    }
                    {/* End of Project Item Component */}
                </div>
            </div>
        </div>
    </div>
            
        );
    }
}

Dashboard.propTypes= {
    project: PropTypes.object.isRequired,
    getProjects: PropTypes.func.isRequired
}

const mapStateToProps = state => ({
    project: state.project

})
export default connect(mapStateToProps, {getProjects })(Dashboard)

```
2. `ProjectItem.js`
```javascript
import React, { Component } from 'react'

export default class ProjectItem extends Component {
    render() {
        const {project} = this.props 
        return (
            <div className="container">
                        <div className="card card-body bg-light mb-3">
                            <div className="row">
                                <div className="col-2">
                                    <span className="mx-auto">{project.projectIdentifier}</span>
                                </div>
                                <div className="col-lg-6 col-md-4 col-8">
                                    <h3>{project.projectName}</h3>
                                    <p>{project.description}</p>
                                </div>
                                <div className="col-md-4 d-none d-lg-block">
                                    <ul className="list-group">
                                        <a href="#">
                                            <li className="list-group-item board">
                                                <i className="fa fa-flag-checkered pr-1">  Project Board </i>
                                            </li>
                                        </a>
                                        <a href="#">
                                            <li className="list-group-item update">
                                                <i className="fa fa-edit pr-1"> Update Project Info</i>
                                            </li>
                                        </a>
                                        <a href="">
                                            <li className="list-group-item delete">
                                                <i className="fa fa-minus-circle pr-1">  Delete Project</i>
                                            </li>
                                        </a>
                                    </ul>
                                </div>
                            </div>
                        </div>
                    </div>
        )
    }
}

```
3. Result
<img src="May8_1.png">

## UpdateProject Form and Route
1. Create UpdateProject
```javascript
import React, { Component } from 'react';

class UpdateProject extends Component {

    render() { 
        return ( 
            <div>
                UpdateProject
            </div>
         );
    }
}
 
export default UpdateProject;
```
2. Add Project Route
`App.js`
```javascript
import React from 'react';
import './App.css';
import Dashboard from './components/Dashboard';
import Header from './components/Layout/Header';
import "bootstrap/dist/css/bootstrap.min.css";
import { BrowserRouter as Router, Route} from "react-router-dom";
import AddProject from './components/Project/AddProject';
import { Provider } from 'react-redux'
import store from './store'
import UpdateProject from './components/Project/UpdateProject'

function App() {
  return (
    <Provider store={store}>
      <Router>
      <div className="App">
        <Header />
        {/* <Dashboard /> */}
        <Route exact path="/addProject" component={AddProject}/>
        <Route exact path="/dashboard" component={Dashboard}/>
        <Route exact path="/updateProject/:id" component={UpdateProject}/>
      </div>
      </Router>
    </Provider>
    
    
  );
}

export default App;

```
3. Add Link in `ProjectItem.js`
```javascript
import React, { Component } from 'react'
import { Link } from 'react-router-dom'

export default class ProjectItem extends Component {
    render() {
        const {project} = this.props 
        return (
            <div className="container">
                        <div className="card card-body bg-light mb-3">
                            <div className="row">
                                <div className="col-2">
                                    <span className="mx-auto">{project.projectIdentifier}</span>
                                </div>
                                <div className="col-lg-6 col-md-4 col-8">
                                    <h3>{project.projectName}</h3>
                                    <p>{project.description}</p>
                                </div>
                                <div className="col-md-4 d-none d-lg-block">
                                    <ul className="list-group">
                                        <a href="#">
                                            <li className="list-group-item board">
                                                <i className="fa fa-flag-checkered pr-1">  Project Board </i>
                                            </li>
                                        </a>
                                        <Link to={`/updateProject/${project.projectIdentifier}`}>
                                            <li className="list-group-item update">
                                                <i className="fa fa-edit pr-1"> Update Project Info</i>
                                            </li>
                                        </Link>
                                        <a href="">
                                            <li className="list-group-item delete">
                                                <i className="fa fa-minus-circle pr-1">  Delete Project</i>
                                            </li>
                                        </a>
                                    </ul>
                                </div>
                            </div>
                        </div>
                    </div>
        )
    }
}

```

4. Update `UpdateProject.js`
```javascript
import React, { Component } from 'react';

class UpdateProject extends Component {

    render() { 
        return ( 
            <div className="container">
                <div className="project">
          <div className="row">
            <div className="col-md-8 m-auto">
              <h5 className="display-4 text-center">Update Project form</h5>
              <hr />
              <form>
                <div className="form-group">
                  <input
                    type="text"
                    className="form-control form-control-lg "
                    placeholder="Project Name"
                  />
                </div>
                <div className="form-group">
                  <input
                    type="text"
                    className="form-control form-control-lg"
                    placeholder="Unique Project ID"
                    disabled
                  />
                </div>
                <div className="form-group">
                  <textarea
                    className="form-control form-control-lg"
                    placeholder="Project Description"
                  />
                </div>
                <h6>Start Date</h6>
                <div className="form-group">
                  <input
                    type="date"
                    className="form-control form-control-lg"
                    name="start_date"
                  />
                </div>
                <h6>Estimated End Date</h6>
                <div className="form-group">
                  <input
                    type="date"
                    className="form-control form-control-lg"
                    name="end_date"
                  />
                </div>

                <input
                  type="submit"
                  className="btn btn-primary btn-block mt-4"
                />
              </form>
            </div>
          </div>
        </div>
      </div>
         );
    }
}
 
export default UpdateProject;
```

## Get Project by Id, Update Use Case Part 1
1. `Types.js`
```javascript
export const GET_ERRORS = "GET_ERRORS"
export const GET_PROJECTS = "GET_PROJECTS"
export const GET_PROJECT = "GET_PROJECT"
```
2. `projectReducer.js`
```javascript
import { GET_PROJECTS } from "../actions/types"
import { GET_PROJECT } from "../actions/types"


const initialState = {
    projects: [],
    project: {}
}

export default function (state = initialState, action) {
    switch (action.type) {
        case GET_PROJECTS:
            return {
                ...state,
                projects: action.payload
            }
    
        case GET_PROJECT:
            return {
                ...state,
                project: action.payload
            }
        default:
            return state;
    }
}
```
3. `projectActions.js`
```javascript
import axios from "axios"
import { GET_ERRORS, GET_PROJECTS, GET_PROJECT} from "./types"

export const createProject = (project, history) => async dispatch => {
    try {
        const res = await axios.post("http://localhost:8080/api/project", project);
        history.push("/dashboard")
    } catch (err) {
        dispatch({
            type:GET_ERRORS,
            payload:err.response.data
        })
    }
}

export const getProjects = () => async dispatch => {
    const res = await axios.get("http://localhost:8080/api/project/all")
    dispatch ({
        type: GET_PROJECTS,
        payload: res.data
    })
}

export const getProject = (id, history) => async dispatch => {
    const res = await axios.get(`http://localhost:8080/api/project/${id}`)
    dispatch({
        type: GET_PROJECT,
        payload: res.data
    })
}
```
4. `UpdateProject.js`
```javascript
import React, { Component } from 'react';
import { getProject } from '../../actions/projectActions'
import PropTypes from 'prop-types'
import { connect } from 'react-redux'
import classnames from 'classnames'

class UpdateProject extends Component {

    componentDidMount () {
        const { id } = this.props.match.params
        this.props.getProject(id, this.props.history)
    }

    render() { 
        return ( 
            <div className="container">
                <div className="project">
          <div className="row">
            <div className="col-md-8 m-auto">
              <h5 className="display-4 text-center">Update Project form</h5>
              <hr />
              <form>
                <div className="form-group">
                  <input
                    type="text"
                    className="form-control form-control-lg "
                    placeholder="Project Name"
                  />
                </div>
                <div className="form-group">
                  <input
                    type="text"
                    className="form-control form-control-lg"
                    placeholder="Unique Project ID"
                    disabled
                  />
                </div>
                <div className="form-group">
                  <textarea
                    className="form-control form-control-lg"
                    placeholder="Project Description"
                  />
                </div>
                <h6>Start Date</h6>
                <div className="form-group">
                  <input
                    type="date"
                    className="form-control form-control-lg"
                    name="start_date"
                  />
                </div>
                <h6>Estimated End Date</h6>
                <div className="form-group">
                  <input
                    type="date"
                    className="form-control form-control-lg"
                    name="end_date"
                  />
                </div>

                <input
                  type="submit"
                  className="btn btn-primary btn-block mt-4"
                />
              </form>
            </div>
          </div>
        </div>
      </div>
         );
    }
}
 
UpdateProject.propTypes = {
    getProject: PropTypes.func.isRequired, 
    project: PropTypes.object.isRequired
}

const mapStateToProps = state => ({
    project: state.project.project
})

export default connect(mapStateToProps, { getProject })( UpdateProject)
```

## Handle Errors in `UpdateProject.js`
1. `projectActions.js`
```javascript
import axios from "axios"
import { GET_ERRORS, GET_PROJECTS, GET_PROJECT} from "./types"

export const createProject = (project, history) => async dispatch => {
    try {
        const res = await axios.post("http://localhost:8080/api/project", project);
        history.push("/dashboard")
    } catch (err) {
        dispatch({
            type:GET_ERRORS,
            payload:err.response.data
        })
    }
}

export const getProjects = () => async dispatch => {
    const res = await axios.get("http://localhost:8080/api/project/all")
    dispatch ({
        type: GET_PROJECTS,
        payload: res.data
    })
}

export const getProject = (id, history) => async dispatch => {
    try {
        const res = await axios.get(`http://localhost:8080/api/project/${id}`)
    dispatch({
        type: GET_PROJECT,
        payload: res.data
    })
    } catch (error) {
        history.push("/dashboard")
    }
    
}
```

2. `UpdateProject.js`
```javascript
import React, { Component } from 'react';
import { getProject, createProject } from '../../actions/projectActions'
import PropTypes from 'prop-types'
import { connect } from 'react-redux'
import classnames from 'classnames'

class UpdateProject extends Component {
    constructor() {
        super()

        this.state = {
            id: "",
            projectName: "",
            projectIdentifier: "",
            description: "",
            start_date: "",
            end_date: "",
            errors: {}
        }
        this.onChange = this.onChange.bind(this)
        this.onSubmit = this.onSubmit.bind(this)
    }

    componentWillReceiveProps(nextProps) {
        if (nextProps.errors) {
            this.setState({ errors: nextProps.errors })
        }
        const {
            id,
            projectName,
            projectIdentifier,
            description,
            start_date,
            end_date
        } = nextProps.project

        this.setState({
            id,
            projectName,
            projectIdentifier,
            description,
            start_date,
            end_date
        })
    }

    componentDidMount () {
        const { id } = this.props.match.params
        this.props.getProject(id, this.props.history)
    }

    onChange(e) {
        this.setState({[e.target.name]:e.target.value})
    }

    onSubmit(e) {
        e.preventDefault()

        const updateProject = {
            id: this.state.id,
            projectName: this.state.projectName,
            projectIdentifier: this.state.projectIdentifier,
            description: this.state.description,
            start_date: this.state.start_date,
            end_date: this.state.end_date
        }

        this.props.createProject(updateProject, this.props.history)
    }

    render() { 
        const { errors } = this.state
        return ( 
            <div className="container">
                <div className="project">
          <div className="row">
            <div className="col-md-8 m-auto">
              <h5 className="display-4 text-center">Update Project form</h5>
              <hr />
              <form onSubmit={this.onSubmit}>
                <div className="form-group">
                  <input
                    type="text"
                    className={classnames("form-control form-control-lg ", {"is-invalid": errors.projectName})}
                    placeholder="Project Name"
                    name="projectName"
                    value={this.state.projectName}
                    onChange={this.onChange}
                  />
                  {
                      errors.projectName && (
                          <div className="invalid-feedback">{errors.projectName}</div>
                      )
                  }
                </div>
                <div className="form-group">
                  <input
                    type="text"
                    className={("form-control form-control-lg", {"is-invalid": errors.projectIdentifier})}
                    placeholder="Unique Project ID"
                    name="projectIdentifier"
                    value={this.state.projectIdentifier}
                    onChange={this.onChange}
                    disabled
                  />
                  {
                      errors.projectIdentifier && (
                          <div className="invalid-feedback">{errors.projectIdentifier}</div>
                      )
                  }
                </div>
                <div className="form-group">
                  <textarea
                    className={("form-control form-control-lg", {"is-invalid": errors.description})}
                    placeholder="Project Description"
                    name="description"
                    onChange={this.onChange}
                    value={this.state.description}
                  />
                  {
                      errors.description && (
                          <div className="invalid-feedback">{errors.description}</div>
                      )
                  }
                </div>
                <h6>Start Date</h6>
                <div className="form-group">
                  <input
                    type="date"
                    className={("form-control form-control-lg", {"is-invalid": errors.start_date})}
                    name="start_date"
                    value={this.state.start_date}
                    onChange={this.onChange}
                  />
                  {
                      errors.start_date && (
                          <div className="invalid-feedback">{errors.start_date}</div>
                      )
                  }
                </div>
                <h6>Estimated End Date</h6>
                <div className="form-group">
                  <input
                    type="date"
                    className="form-control form-control-lg"
                    name="end_date"
                    value={this.state.end_date}
                    onChange={this.onChange}
                  />
                </div>

                <input
                  type="submit"
                  className="btn btn-primary btn-block mt-4"
                />
              </form>
            </div>
          </div>
        </div>
      </div>
         );
    }
}
 
UpdateProject.propTypes = {
    getProject: PropTypes.func.isRequired, 
    project: PropTypes.object.isRequired
}

const mapStateToProps = state => ({
    project: state.project.project,
    errors: state.errors
})

export default connect(mapStateToProps, { getProject, createProject })( UpdateProject)
```
## Delete An Existing project
1. `types.js`

2. `projectReducer.js`

3. `projectAction.js`

4. `ProjectItem.js`

## Refactor Delete Operation and Proxy

1. `package.json`
add
```shell script
  "proxy":"http://localhost:8080"
```

2. Add Confirmation When Delete the Project
`projectActions.js`
```javascript
export const deleteProject = id => async dispatch => {

    if(window.confirm("Are you sure? This will delete the project and all the data related to it")) {
        await axios.delete(`/api/project/${id}`)
    dispatch({
        type: DELETE_PROJECT,
        payload: id
    })
    }
}
```