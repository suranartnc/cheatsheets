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
  switch(action.type) {
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

### Combining multiple reducers

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

A complex app may have multiple reducers. Use `combineReducers()` to combine multiple reducers into one reducer function.

## Usage with React

### Wrapping App with Provider

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
{: data-line="2,3,4"}


The `<Provider>` component makes the store available in your React components. You need this so you can use `connect()`.


### Mapping state to props

```js
import { connect } from 'react-redux'
```
{: .-setup}

```js
function App({ dispatch, counter }) {
  return (
    <div>
      <p>{counter}</p>
      <button onClick={() => { dispatch({ type: 'INCREMENT' })}}>
        +
      </button>
      <button onClick={() => { dispatch({ type: 'DECREMENT' })}}>
        -
      </button>
    </div>
  )
}

function selector(state) {
  return { 
    counter: state 
  }
}

export default connect(selector)(App)
```
`connect()` maps data in the store as component's props and also inject `dispatch()`.

## Middlewares

### Creating a middleware

```js
const myMiddleware = store => next => action { 
  // Before dispatch action
  const result = next(action) 
  // After dispatch action
  return result
}
```

Middlewares are simply decorators for `dispatch()` to allow you to perform different tasks when receiving
actions.

### Applying middlewares

```js
import { createStore, applyMiddleware } from 'redux'
```
{: .-setup}

```js
const enhancer = applyMiddleware(myMiddleware1, myMiddleware2, ...)

const store = createStore(reducer, {}, enhancer)
```
Each middleware will be executed from left to right.

{%endraw%}
