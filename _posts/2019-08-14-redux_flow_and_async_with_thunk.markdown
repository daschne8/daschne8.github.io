---
layout: post
title:      "Redux Flow and async with Thunk"
date:       2019-08-14 16:07:04 -0400
permalink:  redux_flow_and_async_with_thunk
---

Code used in this blog can be found [here](https://github.com/daschne8/redux-flow-demo.git)

Redux allows applications to centralize thier 'state' making persistance easier and facilitating ways to pass that state between components.  While Redux is not limited to React this blog will be talking about Redux in React.

The Redux flow strictly follows 4 basic steps
1. the call
2. the reducer
3. root reducer
4. save complete state

Lets say we had a simple reducer with a counter that starts at 0.
```
state = {count: 0}
```

### 1. the call,

We want to increase the count so we will dispatch the action 
```
{type: "INCREASE_COUNT", amount: 1}
```

### 2. the reducer


```
  export default function simpleReducer(
  state = {count: 0}, action
  ){
  switch (action.type) {
    case 'INCREASE_COUNT':
      return {...state, count: (this.state.count + action.amount)}
    default:
      return state
  }
}
```

the reducer recieves the action in this case the ```action.type``` is ```INCREASE_COUNT``` and the amount is ```1```

### 3. root reducer

the root reducer can combine the multiple reducers output into one state tree, here we use the handy ```combineReducers()``` function. 

```
const rootReducer = combineReducers({
  simple: simpleReducer,
  async: asyncReducer
})
```

### 4. save complete state

the entire state will be saved, in our case it would look like this
```
state = {count: 1}
```

![sync](https://drive.google.com/open?id=1ThyVReo3rzsx2dpJIB_SF04yKPs-_BJ4)
[sync](https://drive.google.com/open?id=1ThyVReo3rzsx2dpJIB_SF04yKPs-_BJ4)

Simple enough, but what if the data we are handling is coming from an api?, what if we have to wait an unknown amount of time for another server to deliver needed data? It would be irresponsible to pause the entire program, what we need is a way to deal with an asynchronous request.

Introduce Redux-Thunk, in proramming "Thunks are primarily used to delay a calculation until its result is needed", redux-thunk allows us to wrap our stores dispatch method and dispatch something other than an action.

first we have to apply the redux-thunk middleware to the store
```
store = createStore(rootReducer, applyMiddleware(thunk))
```

### async call

Lets say we had a program that queries reddit for comments. We can create an action function


```
export function fetchComments(query){
  return(dispatch) => {
    dispatch({type: 'LOADING_COMMENTS'})
    return fetch(`https://www.reddit.com/r/${query}/comments.json`)
      .then(res => {
        if (res.ok) {
          return res.json()
        } else {
          throw new Error('Invald User/Subreddit')
        }})
      .then(data =>
        {const comments = data.data.children.map(child => child.data.body)
        dispatch({type:'FETCH_COMMENTS', payload: comments})})
      .catch((err) => {
        dispatch({type:'THROW_ERROR', payload: err})
      })
  }
}

```

now this is looking a 'bit' more complicated than the synchronous example so lets walk through it,
there is more then one action in this code.  First the function dispatches the action ```LOADING_COMMENTS``` to the reducer(step 1) then the rest of the flow reducer to root reducer rootreducer saves the state.  This will tell us that we are still waiting for our data by setting a variable in the async reducer ```{...state, loading: true}```
It would be a good idea to map the value to a component so it could render some kind of loading indicator. 
 
 ```
 {this.props.loading ? <p>loading please wait . . .</p> : null}
```
in the interim we are waiting for the fetch request to finish, which will depend on reddit's servers.

this means that if i were to take the above code and add some logs to see wherewe are.

```
export function fetchComments(query){
  return(dispatch) => {
    console.log('a')
    dispatch({type: 'LOADING_COMMENTS'})
    fetch(`https://www.reddit.com/r/${query}/comments.json`)
      .then(res => {
        console.log('b');
        if (res.ok) {
          return res.json()
        } else {
          throw new Error('Invald User/Subreddit')
        }})
      .then(data =>
        {console.log('c')
          const comments = data.data.children.map(child => child.data.body)
        dispatch({type:'FETCH_COMMENTS', payload: comments})})
      .catch((err) => {
        console.log('d');
        dispatch({type:'THROW_ERROR', payload: err})
      })
      console.log('e');
  }
}
```
we would see in the console ```//a e b c```
```a``` is at the begining of the function and is logged first
but the fetch request is asynchronous so the rest of our function will run first and log ```e```.  Once the fetch request recieves the response we will log ```b``` and subsequently ```c``` after processing the response as our "data" object.

the second call is made after recieving and processing the response ```FETCH_COMMENTS``` passing in the comments as the ```action.payload``` which goes once again to the reducer => rootReducer => save state, allowing the app to use the data we fetched.

![async](https://drive.google.com/open?id=16Skls5MtHAIw5WLArFFMJkmvmbgYMUgp)
[async](https://drive.google.com/open?id=16Skls5MtHAIw5WLArFFMJkmvmbgYMUgp)

