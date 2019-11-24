---
title: MobX
category: MobX
layout: 2017/sheet
ads: true
tags: [Featured]
updated: 2017-10-10
weight: -10
---

{%raw%}

## Placeholder

## MobX

{: .-two-column}

### Observables (State)

```js
import { observable } from 'mobx'

export default class TodoStore {
  @observable
  todos = []

  // ...
}
```


### Actions (Update state)

```js
import { action } from 'mobx'

export default class TodoStore {
  // ...

  @action
  addTodo(todo) {
    // ...
  }

  @action
  removeTodo(id) {
    // ...
  }
}
```

### Computed Values (Depend on state)

```js
import { observable, computed } from 'mobx'

export default class TodoStore {
  @observable
  todos = []

  @computed
  get totalItems() {
    return this.todos.length
  }
}
```

## Store

### A class that keep state & logics

```bash
File: /features/todo/store.js
```
{: .-setup}

```js
import { uniqueId } from 'lodash'

export default class TodoStore {
  @observable
  todos = []

  @action
  addTodo(todo) {
    this.todos.push({ ...todo, id: uniqueId() })
  }

  @action
  removeTodo(id) {
    this.todos = this.todos.filter(todo => todo.id !== id)
  }

  @computed
  get totalItems() {
    return this.todos.length
  }
}
```


### Register a new store

```bash
File: /lib/store/rootStore.js
```
{: .-setup}

```js
import TodoStore from '@features/todo/store'

export default class RootStore {
  constructor() {
    // ...

    this.todoStore = new TodoStore(this)
  }
}
```

## Observer


### Read state

```js
import React from 'react'
import { inject } from '@lib/store'

function MyComponent({ todoStore }) {
  const { todos, totalItems } = todoStore

  return (
    <div>
      {totalItems > 0 && <TodoList todos={todos} />}
    </div>
  )
}

export default inject('todoStore')(MyComponent)
```

### Write state

```js
import React from 'react'
import { inject } from '@lib/store'

function TodoItem({ todo, todoStore }) {
  const { removeTodo } = todoStore

  return (
    <li>
      <span>{todo.name}</span>
      <button onClick={() => removeTodo(todo.id)}>Remove</button>
    </li>
  )
}

export default inject('todoStore')(MyComponent)
```

{%endraw%}
