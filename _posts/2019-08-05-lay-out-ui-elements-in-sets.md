---
layout: post
title: How to Iterate and Lay Out UI Elements in Sets of X
permalink: /blog/how-to-lay-out-ui-elements-in-sets/
---

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
```

```javascript
const alignByIndex = (index) => {
  const place = index + 1
  const setSize = 3 // the number of items per set
  
  if (place % setSize % 3 === 0) {
    return 'flex-end'
  }
  
  if (place % setSize % 2 === 0) {
    return 'center'
  }
  
  if (place % setSize % 1 === 0) {
    return 'flex-start'
  }
}
```
