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

## JavaScript Arrays

{: .-two-column}

### Adding items

```js
const list = [a, b, c, d, e]
```
{: .-setup}

```js
list.push(X)            // list == [_,_,_,_,_,X]
list.unshift(X)         // list == [X,_,_,_,_,_]
```

```js
list.concat([X,Y])      // return [_,_,_,_,_,X,Y]
```

### Map / Filter

```js
const numbers = [50, 100, 150]
```
{: .-setup}

```js
const numbersWithCurrency = numbers.map(function(number) {
  return number + ' Baht'
})
// ["50 Baht", "100 Baht", "150 Baht"]
```

```js
const numbersOver100 = numbers.filter(function(number) {
  return number > 100
})
// [150]
```

React Components
----------
{: .-three-column}

### Function components

```jsx
function Hello(props) {
  return (
    <div className='message-box'>
      Hello {props.name}
    </div>
  )
}
```
{: data-line="4"}

```jsx
const el = document.body
ReactDOM.render(<Hello name='John' />, el)
```

Functional components have no state. Also, their `props` are passed as the first parameter to a function.

### Class Components

```jsx
class Hello extends React.Component {
  render() {
    return (
      <div className='message-box'>
        Hello {this.props.name}
      </div>
    )
  }
}
```
{: data-line="5"}

Class components can have state and lifecycle. Use `this.props` to access properties passed to the component.

### States

```jsx
constructor(props) {
  super(props)
  this.state = { username: '' }
}
```
{: data-line="3"}

```jsx
this.setState({ username: 'rstacruz' })
```

```jsx
render() {
  this.state.username
  ···
}
```
{: data-line="2"}

Use states (`this.state`) to manage dynamic data.

JSX patterns
------------
{: .-two-column}

### Lists

```jsx
class TodoList extends React.Component {
  render() {
    const { items } = this.props
    return (
      <ul>
        {items.map(item => {
          return <TodoItem key={item.key} item={item} />
        })}
      </ul>
    )
  }
}
```
{: data-line="6,7,8"}

### Conditionals

```jsx
<div>
  {showMyComponent ? <MyComponent /> : <OtherComponent />}
</div>
```

### Short-circuit evaluation

```jsx
<div>
  {showPopup && <Popup />}
</div>
```

### Inner HTML

```jsx
function getHTML() { 
  return "<p>...</p>"; 
}

<div dangerouslySetInnerHTML={{__html: getHTML()}} />
```

### Styling

```jsx
var style = { margin: 0, padding: 0 }
return <div style={style}></div>
```

```jsx
return <div style={{ margin: 0, padding: 0 }}></div>
```

React Lifecycle
---------
{: .-two-column}

### Mounting

| Method | Description |
| --- | --- |
| `constructor` _(props)_ | Initialize state |
| `render()` |
| `componentDidMount()` | Fetch data / Operate on DOM |
| --- | --- |
| `componentWillUnmount()` | Return memory |
| --- | --- |

Set initial the state on `constructor()`.
Add DOM event handlers, timers (etc) on `componentDidMount()`, then remove them on `componentWillUnmount()`.

### Updating

| Method | Description |
| --- | --- |
| `shouldComponentUpdate` *(newProps, newState)* | Return false to skip `render()` |
| `render()` |
| `componentDidUpdate` *(prevProps, prevState)* | Fetch data / Operate on DOM  |

Called when props or states changed.

Advanced React
---------
{: .-two-column}

### Controlled Components

```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props)
    this.state = { keywords: '' }
    this.handleInputChanged = this.handleInputChanged.bind(this)
  }

  handleInputChanged(event) {
    this.setState({ keywords: event.target.value })
  }

  render() {
    return (
      <div>
        <input 
          value={this.state.keywords}
          onChange={this.handleInputChanged}
        />
      </div>
    )
  }
}
```
{: data-line="5,9,16,17"}

### ES7 Class Components

```jsx
class MyComponent extends React.Component {
  state = { keywords: '' }

  handleInputChanged = (event) => {
    this.setState({ keywords: event.target.value })
  }

  render() {
    return (
      <div>
        <input 
          value={this.state.keywords}
          onChange={this.handleInputChanged}
        />
      </div>
    )
  }
}
```
{: data-line="2,4,5,6"}

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
