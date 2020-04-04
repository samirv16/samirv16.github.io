---
layout: post
title:      "Validus Final Project"
date:       2020-04-04 00:43:00 +0000
permalink:  validus_final_project
---


For my last project I decided to build a website dedicated to all the the people who either cant afford a gym membership, or just dont have the time to attend the gym in a regular basis.

The application is a React frontend that communicates with a backend Rails API. The React app was created using 
```
create-react-app
```
The redux store is made available to all components via the `<Provide/>`. I create a redux store with a reducer function and enhancer that allows for thunk middleware:
```
let store = createStore(rootReducer, composeEnhancers(applyMiddleware(thunk)))
```

I use router to ensure the navbar links route to the appropriate URLs, and Switch to make sure it takes us the first matching route:
```
      <Router>
        <Navbar />
        <div className="container">
          <Switch>
            <Route exact path='/' component={Home}/>
            <Route exact path='/workouts' component={Workouts}/>
            <Route exact path="/workouts/new" component={ WorkoutNew } />
            <Route exact path='/about' component={About}/>
          </Switch>
        </div>
      </Router>
```

My reducer sets a default state of an empty array before definining three action types. 
I have a SET-WORKOUT that will get payload as "workouts" and update state accordingly, allowing me to later be able to render existing workouts.
```
export const fetchWorkouts = () => {
    return (dispatch) => {
      return fetch('http://localhost:3000/workouts')
      .then(resp => resp.json())
      .then(workouts => {
        dispatch({type: "SET_WORKOUTS", payload: workouts})
      })
    }
}
```
I also have ADD_WORKOUT and REMOVE_WORKOUT action types that after making corresponding fetch requests allow me to create and delete workouts in the from the database.
My new workout class component contains a constructor that sets state, and a handleChange function to update it with setState. Connect, which is being imported from react-redux, is allowing me to access props in my handle submit function:
```
export default connect(null, { addWorkout })(WorkoutNew)
```
Null has to be passed in becase mapStateToProps is not being used here.
This container is also rendering a form with 3 input fields and submit button:
```
    render() {
        return (
          <Card style={{ opacity: 0.5 }} className="text-center">
          <Form onSubmit={ this.handleSubmit } style={{fontSize: 15}}>
            <h1 >Create Workout</h1>
            <Form.Group >
              <Form.Control  size="lg" placeholder="Name" type="text" name="name" id="name" value={ this.state.name } onChange={ this.handleChange }/>
              <Form.Label htmlFor="name">Workout Name</Form.Label>
            </Form.Group>
            <Form.Group>
              <Form.Control size="lg" placeholder="Description" type="text" name="body" id="body" value={ this.state.body } onChange={ this.handleChange }/>
              <Form.Label htmlFor="body">Workout Description</Form.Label>
            </Form.Group>
            <Form.Group>
              <Form.Control size="lg" placeholder="Rounds" type="integer" name="rounds" id="rounds" value={ this.state.rounds } onChange={ this.handleChange }/>
              <Form.Label htmlFor="rounds">Rounds</Form.Label>
            </Form.Group>
            <Form.Group >
            <Form.Control type="submit" value="Create Workout" className="btn" style={{fontSize: 25}} />
            </Form.Group>
          </Form>
          </Card>
        )
      }
```

In my Workouts container I have class component. It contains componentDidMount method that calls on fetchWorkouts once the components mounts to the DOM. In addition, it renders a list of current workouts. 
```
    render() {
        const workouts = this.props.workouts.map(( workout, i) => <WorkoutItem key={i} workout={workout} />)
        return (
            <Card className="text-center" style={{ opacity: 0.5 }}>
                <Card.Header><h1>Workout List</h1></Card.Header>
                <Card.Body style={{fontSize: 15}}>{workouts}</Card.Body>
            </Card>
        )
    }
```

Finally I have stateless Navbar component that allows me to create and style a navigation bar.
```
const link = {
    width: '150px',
    padding: '12px',
    margin: '0 6px 6px',
    backgroud: 'white',
    textDecoration: 'none',
    color: 'white',
}

const Navbar = () =>
        <Nav variant="tabs" className="justify-content-center" style={{fontSize: 18}}>
                <NavLink to="/" exact style={link} activeStyle={{ background: 'pink' }}>Home</NavLink>
                <NavLink to="/workouts" exact style={link} activeStyle={{background: 'pink'}}>Workouts</NavLink>
                <NavLink to="/workouts/new" exact style={link} activeStyle={{ background: 'pink' }}>New Workout</NavLink>
                <NavLink to="/about" exact style={link} activeStyle={{ background: 'pink' }}>About</NavLink>
        </Nav>
```

I also text component that allows for hard coded text to be rendered in other components, a Home component that contain welcome page content, and an About component with the purpose of informing the user about what the website is about.

