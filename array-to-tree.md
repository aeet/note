---
title: "Array To Tree"
date: "2023-09-03"
categories: 
  - "interview-questions"
  - "pieces-of-knowledge"
coverImage: "689149c3880911ebb6edd017c2d2eca2.png"
---

# Question

Array To Tree

```js
const list = [
  {id: 1, name: '部门1', pid: 0},
  {id: 2, name: '部门1-1', pid: 1},
  {id: 3, name: '部门1-2', pid: 1},
  {id: 4, name: '部门1-1-1', pid: 2},
  {id: 5, name: '部门1-2-1', pid: 3},
  {id: 6, name: '部门2', pid: 0},
  {id: 7, name: '部门2-1', pid: 6},
  {id: 8, name: '部门3', pid: 0},
]
```

# Answer

```js
const list = [
    { id: 1, name: '部门1', pid: 0 },
    { id: 2, name: '部门1-1', pid: 1 },
    { id: 3, name: '部门1-2', pid: 1 },
    { id: 4, name: '部门1-1-1', pid: 2 },
    { id: 5, name: '部门1-2-1', pid: 3 },
    { id: 6, name: '部门2', pid: 0 },
    { id: 7, name: '部门2-1', pid: 6 },
    { id: 8, name: '部门3', pid: 0 },
]

const getChild = (list, result, pid) => {
  for(const item of list) {
    if(item.pid === pid) {
      const newItem = { ...item, children: [] };
      result.push(newItem);
      getChild(list, newItem.children, item.id);
    }
  }
}

const listToTree = (list, pid) => {
  const result = [];
  getChild(list, result, pid);
  return result;
}
const a = listToTree(list, 0)
console.log(a)
```
