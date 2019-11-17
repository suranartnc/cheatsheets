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

## Data Fetching

{: .-two-column}

### Page Component

```bash
File: /pages/repository/[name].js
```
{: .-setup}

```js
function MyPage({ data }) {
  const { full_name, stargazers_count } = data

  return <div>{full_name} stars: {stargazers_count}</div>
}
```

### Set Props for a Page

```js
MyPage.getInitialProps = async (context) => {
  const { query: { name } } = context

  const apiURL = `https://api.github.com/repos/${name}`
  const response = await axios.get(apiURL)

  return { data: response.data }
}
```

## Document Component
{: .-two-column}

```bash
File: /pages/_document.js
```
{: .-setup}

```js
import Document, { Html, Head, Main, NextScript } from 'next/document'

export default class MyDocument extends Document {
  render() {
    return (
      <Html>
        <Head>
          /* Custom code */
        </Head>
        <body>
          <Main />
          <NextScript />
        </body>
      </Html>
    )
  }
}
```

## App Component
{: .-two-column}

### Default

```bash
File: /pages/_app.js
```
{: .-setup}

```js
import App from 'next/app'

class MyApp extends App {
  render() {
    const { Component, pageProps } = this.props

    return <Component {...pageProps} />
  }
}
```

App component never unmounted.

### Custom for Layout

```js
import App from 'next/app'

class MyApp extends App {
  render() {
    const { Component, pageProps } = this.props

    return (
      <Layout>
        <Component {...pageProps} />
      </Layout>
    )
  }
}

function Layout({ children }) {
  return <div className="layout">{children}</div>
}
```


## Static File Serving

```bash
Image file: /public/logo.png
```
{: .-setup}

```js
function Logo() {
  return (
    <a href="#">
      <img src="/logo.png" alt="Logo" />
    </a>
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
