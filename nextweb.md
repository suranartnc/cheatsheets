---
title: NextWeb.js
category: Next.js
layout: 2017/sheet
ads: true
tags: [Featured]
updated: 2017-10-10
weight: -10
---

{%raw%}

## Placeholder

## Named Routes

{: .-two-column}

### Route Configuration

```bash
File: /router/routes/_main.js
```
{: .-setup}

```js
const routes = [
  {
    pattern: '/',               // URL
    name: 'home',               // Route Name
    page: 'index'               // Page Filename
  }, {
    pattern: '/contact-us',
    name: 'contact-us',
  }, {
    pattern: '/article/:id',    // Use ":" to make it a parameter
    name: 'article-detail',
  }
]
```


### Links

```js
import Link from '@link'

function MyComponent() {
  return (
    <div>
      <Link route="home">
        <a>Home</a>
      </Link>
      <Link route="article-detail" params={{ id: 1234 }}>
        <a>Article ID: 1234</a>
      </Link>
    </div>
  )
}
```


## Data Fetching using Services

{: .-two-column}

### Server-side

```js
import * as ArticleService from '@features/article/services'

function ArticleSearchResultsPage({ data }) {
  // ...
}

ArticleSearchResultsPage.getInitialProps = async (context) => {
  const { query: { keyword } } = context
  const data = await ArticleService.getArticlesByKeyword(keyword)
  return { data }
}
```

### Client-side


```js
import { useRouter } from 'next/router'
import { Fetch } from '@lib/api'
import * as ArticleService from '@features/article/services'

function ArticleListSection() {
  const { query: { keyword } } = useRouter()

  return (
    <div>
      <Fetch service={() => ArticleService.getArticlesByKeyword(keyword)}>
        {({ data }) => <ArticleList data={data} />}
      </Fetch>
    </div>
  )
}
```

### Head Management

```js
ArticleDetailPage.getInitialProps = async (context) => {
  const { query: { id } } = context
  const data = await ArticleService.getArticleById(id)
  return { 
    data,
    title: data.title,
    meta: {
      description: data.description,
      keywords: data.keywords
    }
  }
}
```


## Styling
{: .-two-column}

### Local Scoped
```js
function MyComponent() {
  return (
    <div css={{ color: '#ff0000', paddingTop: '10px' }}>
      Some Text
    </div>
  )
}
```

### Global Scoped

```bash
File: /lib/styles/GlobalStyles.js
```
{: .-setup}

```js
import { css, Global } from '@emotion/core'

const baseStyles = css`
  /* Add global styles here... */
`
```

## Grids
{: .-two-column}

### Basic

```js
import { Flex, Box } from '@grid'

function MyComponent() {
  return (
    <Flex>
      <Box width={1/2}>
        Width 50%
      </Box>
      <Box width={1/2}>
        Width 50%
      </Box>
    </Flex>
  )
}
```

### Responsive

```js
import { Flex, Box } from '@grid'

function MyComponent() {
  return (
    <Flex>
      <Box width={[1, 2/3]}>
        Width 100% (Mobile) | Width 66.66% (Desktop)
      </Box>
      <Box width={[1, 1/3]}>
        Width 100% (Mobile) | Width 33.33% (Desktop)
      </Box>
    </Flex>
  )
}
```

{%endraw%}
