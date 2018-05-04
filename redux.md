---
title: React.js
category: React
layout: 2017/sheet
ads: true
tags: [Featured]
updated: 2017-10-10
weight: -10
keywords:
  - React.Component
  - render()
  - componentDidMount()
  - props/state
  - dangerouslySetInnerHTML
---

{%raw%}

## Placeholder

Redux
---------
{: .-two-column}

### Creating a store

```js
import { createStore } from 'redux'
```
{: .-setup}

```js
// Reducer for counter app
function reducer(state = 0, action) {
  switch (action.type) {
    case 'INCREMENT':
      return state + 1
    case 'DECREMENT':
      return state - 1
    default:
      return state
  }
}

const store = createStore(reducer)
```

A store is made from a reducer function, which takes the current `state`, and returns a new `state` depending on the `action` it was given.

### Using a store

```js
// Dispatches actions
store.dispatch({ type: 'INCREMENT' })
store.dispatch({ type: 'DECREMENT' })
```

```js
// Gets the current state
store.getState()
```

```js
// Listens for changes
store.subscribe(() => {
  console.log(store.getState()) 
})
```

Dispatch actions to change the store's state.

### Combining reducers

```js
import { createStore, combineReducers } from 'redux'
```
{: .-setup}

```js
const reducer = combineReducers({
  counter: counterReducer, 
  user: userReducer,
  ... 
})

const store = createStore(reducer)
```

Combines multiple reducers into one reducer function.

## React Redux

### Provider

```js
import { Provider } from 'react-redux'
```
{: .-setup}

```js
React.render(
  <Provider store={store}>
    <App />
  </Provider>, 
  mountNode
)
```

The `<Provider>` component makes the store available in your React components. You need this so you can use `connect()`.


### Mapping state to props

```js
import { connect } from 'react-redux'
```
{: .-setup}

```js
function App({ dispatch, message }) {
  return (
    <div onClick={() => {
      dispatch({ 
        type: 'click', 
        message: 'hello' 
      })
    }}>
      {message}
    </div>
  )
}

function selector(state) {
  return { 
    message: state.message 
  }
}

export default connect(selector)(App)
```

## Middleware

### Creating a middleware

```js
const myMiddleware = store => next => action { 
  return next(action) 
}
```

Middlewares are simply decorators for `dispatch()` to allow you to take
different kinds of actions, and to perform different tasks when receiving
actions.

### Applying middleware

```js
import { createStore, applyMiddleware } from 'redux'
```
{: .-setup}

```js
const enhancer = applyMiddleware(myMiddleware1, myMiddleware2, ...)

const store = createStore(reducer, {}, enhancer)
```

{%endraw%}
