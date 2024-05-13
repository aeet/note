---
title: "Summary of 《Hello, Algorithm》- 12"
date: "2024-03-26"
categories: 
  - "algorithm"
  - "hello-algorithm"
tags: 
  - "algorithm"
coverImage: "f7b45c9a0b794c789877e1d687d4ef76.jpg"
---

# Graph traversal

- Trees represent a "one-to-many" relationship, while graphs have a higher degree of freedom and can represent any "many-to-many" relationship.

# breadth-first traversal

- Breadth-first traversal is a traversal method from near to far. Starting from a certain node, it always gives priority to visit the nearest vertex and expands outward layer by layer.

```c++
/* Breadth-first traversal */
// Use an adjacency list to represent the graph to obtain all adjacent vertices of a specified vertex
vector<Vertex *> graphBFS(GraphAdjList &graph, Vertex *startVet) {
    // Vertex traversal sequence
    vector<Vertex *> res;
    // Hash table, used to record the vertices that have been visited
    unoredered_set<Vertex *> visited = {startVet};
    // Queue is used to implement BFS
    queue<Vertex *> que;
    que.push(startVet);
    while(!que.empty()){
        Vertex *vet = que.front();
        // The first vertex of the team leaves the tea
        que.pop();
        // Record visited vertices
        res.push_back(vet);
        // Traverse all adjacent vertices of this vertex
        for(auto adjVet : graph.adjList[vet]){
              if (visited.count(adjVet))
                  // Skip already visited vertices
                continue;
              // Only enqueue unvisited vertices
              que.push(adjVet);
              // Mark the vertex as visited
              visited.emplace(adjVet);
        }
    }
    // Return the vertex traversal sequence
    return res;
}
```

# depth first traversal

- Depth-first traversal is a traversal method that prioritizes going to the end and turning back when there is no way to go.

```cpp
void dfs(GraphAdjList &graph, unordered_set<Vertex *> &visited, vector<Vertex *> &res, Vertex *vet) {
    res.push_back(vet);
    visited.emplace(vet);
    for (Vertex *adjVet : graph.adjList[vet]) {
        if (visited.count(adjVet))
            continue;
        dfs(graph, visited, res, adjVet);
    }
}

vector<Vertex *> graphDFS(GraphAdjList &graph, Vertex *startVet) {
   vector<Vertex *> res;
   unordered_set<Vertex *> visited;
   dfs(graph, visited, res, startVet);
   return res;
}
```
