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

### Backtick strings

```js
const message = `Hello ${name}`
```

### Arrow Functions

```js
const greet = (name = 'Tae') => {
  return `Hello ${name}`
}
```

### Destructuring


```js
// Objects

const { title, author } = {
  title: 'React.js Essentials',
  author: 'Suranart Niamcome'
}
```


```js
// Arrays

const [first, second] = ['Nikola', 'Tesla']
```

### Spread

```js
// Objects

const options = { ...defaultOptions, someKey: 'Overriding value' }
```

```js
// Arrays

const users = [ ...admins, ...editors, 'New user' ]
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
  .then(data => { console.log(data) })
```

### Fetch options

```js
fetch('/data.json', {
  method: 'post',
  body: JSON.stringify(...),
  headers: { 'Accept': 'application/json' }
})
```

{%endraw%}
