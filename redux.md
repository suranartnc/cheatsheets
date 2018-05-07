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

### Applying middlewares

```js
import { createStore, applyMiddleware } from 'redux'
```
{: .-setup}

```js
const enhancer = applyMiddleware(myMiddleware1, myMiddleware2, ...)

const store = createStore(reducer, {}, enhancer)
```

{%endraw%}
