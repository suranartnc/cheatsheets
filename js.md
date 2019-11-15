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
}) // ["50 Baht", "100 Baht", "150 Baht"]
```

```js
const numbersOver100 = numbers.filter(function(number) {
  return number > 100
}) // [150]
```

## Modern JavaScript

{: .-two-column}

### Block Scoped Declarations

```js
let counter = 0
counter++
```

```js
const counter = 0
counter++               // Error: "counter" is read-only
```

Both ***let*** and ***const*** are scoped to ***{}***.

### Template Literals

```js
const name = 'JavaScript'
const message = `Hello, ${name}`
```

### Destructuring

```js
// Objects
const book = {
  title: 'JavaScript Essentials',
  author: 'Suranart Niamcome'
}

const { title, author } = book
```

```js
// Arrays
const [first, second] = ['Nikola', 'Tesla']
```

### Arrow Functions

```js
const greet = (name = 'JavaScript') => {
  return `Hello, ${name}`
}
```

## Modules

{: .-two-column}

### Default exports (one per module)

```js
// myLibrary.js
export default function() { ··· }
```

```js
import myLibrary from './myLibrary.js'
```

### Named exports (several per module)

```js
// myHelpers.js
export function mymethod1() { ··· }
export function mymethod2() { ··· }
export function mymethod3() { ··· }
```

```js
import { mymethod1, mymethod2 } from './myHelpers.js'
```

## Promises

{: .-two-column}

### Creating promises

```js
function doSomethingAsync() {
  return new Promise((resolve, reject) => {
    // do async task...
    if (error) {
      reject(error)     // failure
    } else {
      resolve(result)   // success
    }
  })
}
```

A Promise wraps asynchronous code into an object that has a method ***then()*** to get the result of code execution.

### Using promises

```js
doSomethingAsync()
  .then(result => { 
    // use result from async operation
  })
  .catch(error => { 
    // handle error
  })
```

### Fetch API using Axios

```js
import axios from 'axios
const apiUrl = 'https://api.github.com/repos/facebook/react'

axios.get(apiUrl)
  .then(response => { 
    console.log(response.data)
  })
  .catch(error => { 
    console.log(error)
  })
```

{%endraw%}
