---
layout: post
title: How to Iterate and Lay Out UI Elements in Sets of X
permalink: /blog/how-to-lay-out-ui-elements-in-sets/
---

Let's say you have a list of items that you need to render diagonally in sets
of three, like so:

```
1
 2
  3
4
 5
  6
7
 8
  9

etc.
```

You can use the modulo operator to determine the placement of each individual
list item:

```javascript
const alignByIndex = (index) => {
  const place = index + 1
  const numberOfItemsPerSet = 3
  
  if (place % numberOfItemsPerSet % 3 === 0) {
    return 'flex-end'
  }
  
  if (place % numberOfItemsPerSet % 2 === 0) {
    return 'center'
  }
  
  if (place % numberOfItemsPerSet % 1 === 0) {
    return 'flex-start'
  }
}
```

If you want to have sets of four, you only need to set `numberOfItemsPerSet`
to `4` and write an if condition for the fourth item.

Here's an example of how you would use it inside a React component:

```jsx
const DiagonalItems = ({items}) =>
  <ul style={...}>
    {
      items.map((item, index) =>
        <li key={item.id} style={{alignSelf: alignByIndex(index)}}>
          {item.title}
        </li>
      )
    }
  </ul>
```
