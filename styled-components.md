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

## Ant Design

{: .-two-column}

### Grid
```js
import { Row, Col } from 'antd'
```
{: .-setup}

```js
ReactDOM.render(
  <div>
    <Row>
      <Col span={12}>col-12</Col>
      <Col span={12}>col-12</Col>
    </Row>
    <Row>
      <Col span={8}>col-8</Col>
      <Col span={8}>col-8</Col>
      <Col span={8}>col-8</Col>
    </Row>
  </div>
, mountNode);
```

### Responsive Grid
```js
import { Row, Col } from 'antd'
```
{: .-setup}

```js
ReactDOM.render(
  <Row>
    <Col xs={2} sm={4} md={6} lg={8} xl={10}>Col</Col>
    <Col xs={20} sm={16} md={12} lg={8} xl={4}>Col</Col>
    <Col xs={2} sm={4} md={6} lg={8} xl={10}>Col</Col>
  </Row>
, mountNode);
```

## Styled Components

{: .-two-column}

### With HTML Tags

```js
import styled from 'styled-components'
```
{: .-setup}

```js
const Title = styled.h1`
  font-size: 1.5em;
  text-align: center;
  color: red;
`;

const Wrapper = styled.section`
  padding: 4em;
  background: green;
`;

render(
  <Wrapper>
    <Title>
      Hello World, this is my first styled component!
    </Title>
  </Wrapper>
);
```

### With React Components

```js
const Link = ({ className, children }) => (
  <a className={className}>
    {children}
  </a>
)

const StyledLink = styled(Link)`
  color: red;
  font-weight: bold;
`;

render(
  <div>
    <Link>Unstyled, boring Link</Link>
    <br />
    <StyledLink>Styled, exciting Link</StyledLink>
  </div>
);
```

## Styled Components (Advanced)

### Based on props

```js
const Button = styled.button`
  background: ${props => props.primary ? 'black' : 'white'};
  color: ${props => props.primary ? 'white' : 'black'};
`;

render(
  <div>
    <Button>Normal</Button>
    <Button primary>Primary</Button>
  </div>
);
```



### Extend

```js
const Button = styled.button`
  color: black;
  padding: 0.25em 1em;
  border: 2px solid black;
  border-radius: 3px;
`;

const RedButton = Button.extend`
  color: red;
  border-color: red;
`;

render(
  <div>
    <Button>Normal Button</Button>
    <RedButton>Red Button</RedButton>
  </div>
);
```

### Attrs

```js
const Input = styled.input.attrs({
  type: 'password',
  margin: props => props.size || '1em',
  padding: props => props.size || '1em'
})`
  color: red;
  font-size: 1em;
  border: 2px solid red;
  border-radius: 3px;
  margin: ${props => props.margin};
  padding: ${props => props.padding};
`;

render(
  <div>
    <Input placeholder="A small text input" size="1em" />
    <Input placeholder="A bigger text input" size="2em" />
  </div>
);
```

### Global Styles

```js
import { injectGlobal } from 'styled-components';
```
{: .-setup}

```js
injectGlobal`
  @font-face {
    font-family: 'Operator Mono';
    src: url('../fonts/Operator-Mono.ttf');
  }
  body {
    margin: 0;
  }
`;
```

{%endraw%}
