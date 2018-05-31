---
title: Next.js
category: Next.js
layout: 2017/sheet
ads: true
tags: [Featured]
updated: 2017-10-10
weight: -10
---

{%raw%}

## Placeholder

## Next.js

{: .-two-column}

### Routes

```bash
File: ./routes.js
```
{: .-setup}

```js
const routes = [
  {
    name: 'home',
    pattern: '/',
    page: 'index'
  }, {
    name: 'about',
    pattern: '/about/',
  }, {
    name: 'entry',
    pattern: '/:id(\\d+)/',
  }
]
```


### Link

```js
import { Link } from './routes'
```
{: .-setup}

```js
function MyComponent() {
  return (
    <div>
      <Link route="home">
        <a>Home</a>
      </Link>
      <Link route="entry" params={{ id: 1234 }}>
        <a>Entry: 1234</a>
      </Link>
    </div>
  )
}
```


## Data Fetching

{: .-two-column}

### getInitialProps

```js
import axios from 'axios
const api = 'https://api.github.com/repos/zeit/next.js'
```
{: .-setup}

```js
class MyPage extends React.Component {
  static async getInitialProps() {
    const response = await axios.get(api)
    return { data: response.data }
  }

  render() {
    const { data } = this.props
    // ...
  }
}
```

### Context

```js
class MyPage extends React.Component {
  static async getInitialProps(context) {
    const { pathname, asPath, query, req, res } = context
    const response = await axios.get(`${api}?id=${query.id}`)
    // ...
  }

  render() {
    // ...
  }
}
```

## Custom...
{: .-two-column}

### Document
```bash
File: ./pages/_document.js
```
{: .-setup}

```js
import Document, { Head, Main, NextScript } from 'next/document'

export default class MyDocument extends Document {
  render() {
    return (
      <html>
        <Head>
          <style>{`body { margin: 0 } /* custom! */`}</style>
        </Head>
        <body className="custom_class">
          <Main />
          <NextScript />
        </body>
      </html>
    )
  }
}
```

### App

```bash
File: ./pages/_app.js
```
{: .-setup}

```js
import App, { Container } from 'next/app'

class MyApp extends App {
  render() {
    const { Component, pageProps } = this.props

    return (
      <Container>
        <Component {...pageProps} />
      </Container>
    )
  }
}
```

### Head

```bash
import Head from 'next/head'
```
{: .-setup}

```js
function EntryPage() {
  return (
    <div>
      <Head>
        <title>Entry: 1234</title>
      </Head>
      <p>Hello world!</p>
    </div>
  )
}
```

## Styling

### Built-in
```js
function MyComponent() {
  return (
    <div>
      Hello world
      <p>scoped!</p>

      <style jsx>{`
        p { color: blue; }
        div { background: red; }
      `}</style>

      <style global jsx>{`
        body { background: black; }
      `}</style>

    </div>
  )
}
```

### Static File
```js
function Logo() {
  return (
    <header>
      <img src="/static/logo.png" alt="Logo" />
    </header>
  )
}
```

<!-- ## Configurations
{: .-two-column}

### Next.js + Webpack

```bash
File: ./next.config.js
```
{: .-setup}

```js
const isProd = process.env.NODE_ENV === 'production'

module.exports = {
  distDir: 'build',
  assetPrefix: isProd ? 'https://cdn.mydomain.com' : '',
  webpack: (config, { buildId, dev, isServer, defaultLoaders }) => {
    // Perform customizations to webpack config

    // Important: return the modified config
    return config
  }
}
```

### Babel
```bash
File: ./.babelrc
```
{: .-setup}


```js
{
  "presets": ["next/babel"],
  "plugins": []
}
``` -->

{%endraw%}
