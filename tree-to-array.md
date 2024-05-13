---
title: "Tree To Array"
date: "2023-09-02"
categories: 
  - "interview-questions"
  - "pieces-of-knowledge"
tags: 
  - "subject"
  - "typescript"
coverImage: "141db7adc52b42d3a00d0f95625d047b.jpg"
---

# Question

Convert the data of the following structure into an array.

```js
const listTree = [
  {
    id: 1,
    name: '部门1',
    pid: 0,
    children: [
      {
        id: 2,
        name: '部门1-1',
        pid: 1,
        children: [
          {
            id: 4, 
            name: '部门1-1-1', 
            pid: 2,
            children: []
          }
        ]
      },
      {
        id: 3,
        name: '部门1-2',
        pid: 1,
        children: [
          {
            id: 5, 
            name: '部门1-2-1', 
            pid: 3,
            children: []
          }
        ]
      }
    ]
  },
  {
    id: 6,
    name: '部门2',
    pid: 0,
    children: [
      {
        id: 7, 
        name: '部门2-1', 
        pid: 6,
        children: []
      }
    ]
  },
  {
    id: 8,
    name: '部门3',
    pid: 0,
    children: []
  }
]
```

# Answer

```ts
const trans = (list: any[], result: Array<any>): void => {
    list.forEach(l => {
        if (l.children && l.children.length > 0) {
            trans(l.children, result)
            delete l.children
        }
        result.push(l)
    })
}

const unzip = (list: any[]): any[] => {
    let queen: any[] = []
    const result: any[] = []
    queen = queen.concat(list)
    while (queen.length) {
        const first = queen.shift()
        if (first["children"] && first["children"].length > 0) {
            queen = queen.concat(first["children"])
            delete first["children"]
        }
        result.push(first);
    }
    return result;
}
```
