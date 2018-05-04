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

## Modern JavaScript

{: .-two-column}

### Backtick strings

```js
const message = `Hello ${name}`
```

### Arrow Functions

```js
const greet = (name = 'Jerry') => {
  return `Hello ${name}`
}
```

### Destructuring

#### Objects

```js
let { title, author } = {
  title: 'React.js Essentials',
  author: 'Suranart Niamcome'
}
```
{: data-line="1"}

#### Arrays

```js
const [first, second] = ['Nikola', 'Tesla']
```
{: data-line="1"}

### Spread

#### Object
```js
const options = {
  ...defaults,
  someKey: 'Overriding value'
}
```
{: data-line="2"}

#### Array

```js
const users = [
  ...admins,
  ...editors,
  'New user'
]
```
{: data-line="2,3"}

## Promises

{: .-two-column}

### Creating promises

```js
function doSomethingAsync() {
  return new Promise((resolve, reject) => {
    // do async task

    if (error) {
      reject(error)     // failure
    } else {
      resolve(result)   // success
    }
  })
}
```
{: data-line="6,8"}

### Using promises

```js
doSomethingAsync()
  .then(function(result) { 
    // use result from async operation
  }, function(reason) { 
    // handle operational errors
  })
  .catch(function(error) { 
    // handle programming errors
  })
```

### Using promises with Async / Await

```js
async function doMoreThing() {
  const result = await doSomethingAsync()
  // use result from async operation
  ...
}
```

## Fetch

{: .-two-column}

### Fetch

```js
import 'isomorphic-unfetch'
```
{: .-setup}

```js
fetch('/data.json')
  .then(response => response.json())
  .then(data => {
    console.log(data)
  })
```
{: data-line="4"}

### Fetch options

```js
fetch('/data.json', {
  method: 'post',
  body: JSON.stringify(...),
  headers: {
    'Accept': 'application/json'
  }
})
```

{%endraw%}
