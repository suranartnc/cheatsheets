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
intro: |
  [React](https://reactjs.org/) is a JavaScript library for building user interfaces. This guide targets React v15 to v16.
---

{%raw%}

Components
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

Class components can have state and lifecycle. Use `this.props` to access properties passed to the component.

### States

```jsx
constructor(props) {
  super(props)
  this.state = { username: '' }
}
```

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
{: data-line="7,8,9"}

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

Lifecycle
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

Advanced
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

{%endraw%}
