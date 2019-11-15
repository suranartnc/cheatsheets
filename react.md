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

Components
----------
{: .-three-column}

### Create a component

```jsx
import React from 'react'

function Hello(props) {
  return (
    <div>
      Hello, {props.name}
    </div>
  )
}
```

### Render the component

```jsx
import React from 'react'
import ReactDOM from 'react-dom'

const el = document.body
ReactDOM.render(<Hello name="John" />, el)
```

### Styling

```jsx
const style = { margin: 0, padding: 0 }

function Hello(props) {
  return (
    <div style={style}>
      Hello, {props.name}
    </div>
  )
}
```

JSX Expressions
------------
{: .-two-column}

### Lists

```jsx
function BookList(props) {
  const { books } = props

  return (
    <ul>
      {books.map(book => {
        return <BookItem key={book.id} book={book} />
      })}
    </ul>
  )
}
```

### Conditional Rendering (Inline)

```jsx
<div>
  {showMyComponent ? <MyComponent /> : <OtherComponent />}
</div>
```



### Conditional Rendering


```jsx
function BookList(props) {
  const { books } = props

  if (books.length === 0) {
    return <div>There is no book.</div>
  }

  return (
    <ul>
      {books.map(book => {
        return <BookItem key={book.id} book={book} />
      })}
    </ul>
  )
}
```


### Short-circuit Evaluation

```jsx
<div>
  {showMyComponent && <MyComponent />}
</div>
```






State
---------
{: .-two-column}

### Events
```jsx
function MyComponent() {
  const fetchData = function() {
    console.log('Fetch data')
  }

  return (
    <div>
      <button onClick={fetchData}>Fetch</button>
    </div>
  );
}
```

### State
```jsx
import React, { useState } from 'react'

function MyComponent() {
  const [counter, setCounter] = useState(0)
  const increaseCounter = function() {
    setCounter(counter + 1)
  }

  return (
    <div>
      <p>{counter}</p>
      <button onClick={increaseCounter}>Count</button>
    </div>
  );
}
```

Updating the state is not allowed inside the main body of a function component, put your code inside an event handler or an effect instead.

### Controlled Components

```jsx
import React, { useState } from 'react'

function MyComponent() {
  const [keyword, setKeyword] = useState('')

  const onKeywordChanged = function(event) {
    setKeyword(event.target.value)
  }

  return (
    <div>
      <input value={keyword} onChange={onKeywordChanged} />
    </div>
  )
}
```

Side Effects
---------
{: .-two-column}

### Create an effect
```jsx
import React, { useState, useEffect } from 'react'

function MyComponent() {
  const [counter, setCounter] = useState(0)

  useEffect(() => {
    setTimeout(() => {
      setCounter(counter + 1)
    }, 1000)
  })

  return <div>{counter}</div>
}
```

A side effect is an expensive task such as data fetching, DOM manipulation, subscription, etc.

### Effect with Cleanup and Dependency
```jsx
import React, { useState, useEffect } from 'react'

function MyComponent() {
  const [counter, setCounter] = useState(0)

  useEffect(() => {
    // Effect (After DOM update)
    const timeoutId = setTimeout(() => {
      setCounter(counter + 1)
    }, 1000)

    return () => {
      // Cleanup (After unmount + Before next update)
      clearTimeout(timeoutId)
    }
  }, [counter]) // Dependency

  return <div>{counter}</div>
}
```

{%endraw%}
