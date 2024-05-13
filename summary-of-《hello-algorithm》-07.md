---
title: "Summary of 《Hello, Algorithm》- 07"
date: "2023-12-25"
categories: 
  - "algorithm"
  - "hello-algorithm"
tags: 
  - "algorithm"
coverImage: "717d527514dc41e58a9ab23269912617.jpg"
---

# binary tree

```
          A
        /   \
       B     C
      / \   / \
     D   E F   G
```

- non-linear data structures.
- the basic unit of a binary tree is a node.
    - each node contains a value.
    - a left child node reference.
    - a right child node reference.

```cpp
struct TreeNode{
    int val;
    TreeNode *left;
    TreeNode *right;

}
```

- in a binary tree, except leaf nodes, all other nodes contain child nodes, and non-empty subtrees.
    
- binary tree common terms
    
    - root node: the node located at the top level of the binary tree has no parent node.
    - leaf node: a node without child nodes, both of its pointers point to None.
    - edge: the line segment connecting two nodes, that is, the node reference(pointer).
    - level: increasing from the top to bottom, the level of the root node is 1.
    - degree: the number of child nodes of the node. in binary tree, the degree range is 0, 1, and 2.
    - depth: the number of edges from the root node to the node.
    - tree height: the number of edges from the root node to the farthest leaf node.
    - node height: the number of edges from the furthest leaf node to the node.

# common binary tree types

- perfect binary tree
    - in a perfect binary tree, the degree of a leaf node is `0` and the degree of all other nodes is `2`.
    - if the height of the tree is `h`, the total number of notes is `2^{h+1}-1`, showing a standard exponential relationship.
- complete binary tree
    - only the bottom node is not filled, and the bottom node is as far to the left as possible filling.
- full binary tree
    - except for leaf nodes, all other nodes have two child nodes.
- balanced binary tree
    - the absolute value of the difference between the height of the left subtree and right subtree of any node is not more than `1`.

|  | perfect binary tree | linked list |
| --- | --- | --- |
| the number of nodes in layer `i` | `2^{i-1}` | 1 |
| the number of leaf nodes of a tree with height `h` | `2^h` | 1 |
| the total number of nodes in a tree with height `h` | `2^{h+1}-1` | `h+1` |
| the height of a tree with total number of nodes `n` | `log_2(n+1)-1` | `n-1` |

# binary tree traversal

## level-order traversal

- traverse the binary tree layer by layer from top to bottom, and follow the steps from left to right at each layer.
- level-order traversal essentially belongs to `breadth-first traversal`, also know as `breadth-first search - BFS`, which embodies a layer-by-layer traversal method of `expanding outward in circles`.

```cpp
vector<int> levelOrder(TreeNode *root){
    queue<TreeNode *> queue;
    queue.push(root);
    vector<int> vec;
    while(!queue.empty()){
        TreeNode *node = queue.front();
        queue.pop();
        vec.push_back(node->val);
        if( node->left != nullptr){
            queue.push(node->left);
        }
        if( node->right != nullptr){
            queue.push(node->right);
        }
    }
    return vec;
}
```

- the time complexity is `O(n)`: all nodes are visited once, using `O(n)` time, where `n` is the number of nodes.
- in the worst case, that is, when the binary tree is full, before traversing to the bottom level, there are at most `(n+1)/2` nodes in the queue at the same time, occupying `O(n)` space.

## pre-order, in-order and post-order traversal

- all belong to `depth-first traversal - DFT`

```
          A
        /   \
       B     C
      / \   / \
     D   E F   G
```

- pre-order: A,B,D,E,C,F,G
- in-order: D,B,E,A,F,C,G
- post-order: D,E,B,F,G,C,A

```cpp
// pre order
// A -> B -> D -> E -> C -> F -> G
void preOrder(TreeNode *root){
    if(root == nullptr)
        return;
    vec.push_back(root->val);
    preOrder(root->left);
    preOrder(root->right);
}

// in order
// D -> B -> E -> A -> C -> F -> G
void inOrder(TreeNode *root){
    if(root == nullptr)
        return;
    inOrder(root->left);
    vec.push_back(root->val);
    inOrder(root->right);
}

// post-order
// D -> E -> B -> F -> G -> C -> A
void postOrder(TreeNode *root){
    if(root == nullptr)
        return;
    postOrder(root->left);
    postOrder(root->right);
    vec.push_bakc(root->val);
}
```

- the time complexity is `O(n)`: all nodes are visited once, using `O(n)` time.
- the space complexity is `O(n)`: in the worst case, when the ree degenerates into a linked list, the recursion depth reaches `n` and the system occupies `O(n)` stack frame space.
