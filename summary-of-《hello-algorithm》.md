---
title: "Summary of 《Hello, Algorithm》- 01"
date: "2023-11-24"
categories: 
  - "algorithm"
  - "hello-algorithm"
tags: 
  - "algorithm"
coverImage: "7fd3279764cc4f07ba703aa2b06c5d2f.jpg"
---

# Complexity Analysis

## Algorithm Efficiency Evaluation

- objectives on two levels.
    - to find a solution to the problem: reliably obtainling solutions within a specified range.
    - seeking the optimal solution: find the fatest one among numberous solutions.
- two dimensions.
    - time efficiency: algorithm execution speed.
    - space efficiency: algorithm memory usage.

## Time Complexity

time complexity analysis does not measure the actual running time of an algorithm but rather the growth trend of the running time as the size of the input data increases.

example

```c++
# constant time complexity
void algorithm_A(int n) {
    cout << 0 << endl;
}

# linear time complexity
void algorithm_B(int n) {
    for (int i = 0; i < n; i++) {
        cout << 0 << endl;
    }
}

# constant time complexity
void algorithm_C(int n) {
    for (int i = 0; i < 1000000; i++) {
        cout << 0 << endl;
    }
}
```

## Asymptotic upper bound / Big O Notation

```c++
void algorithm(int n){
    int a = 1; // one operation
    a = a + 1; // one operation
    a = a * 2; // one operation
    // loop n times
    for(int i = 0; i < n;i++){ // i++ one operation
        count << 0 << endl; // one operation
    }
}
```

Let the operation count of the algorithm be a function of the input data size `n`, denoted as `T(n)`.

`T(n) = 3 + 2n`.

`𝑇(𝑛)` is a linear function, indicating that its running time grows linearly; therefore, its time complexity is linear.

we denote the time complexity of linear order as `𝑂(𝑛)`. This mathematical notation is called `big‑𝑂 notation` representing the asymptotic upper bound of the function `𝑇(𝑛)`.

> Asymptotic Upper Bound: If there exist positive real numbers `𝑐` and `𝑛0`, such that for all `𝑛 > 𝑛0`, it holds that `𝑇(𝑛) ≤ 𝑐 ⋅ 𝑓(𝑛)`, then it can be considered that `𝑓(𝑛)` provides an asymptotic upper bound for `𝑇(𝑛)`, denoted as `𝑇(𝑛) = 𝑂(𝑓(𝑛))`.

## Interface Method

### Step one: counting the number of operations.

> technique tips: The constant term `𝑐` can take any value, so various coefficients and constant terms in the operation count `𝑇(𝑛)` can be ignored.
> 
> - ignoring the constant terms in `𝑇(𝑛)`.
> - omitting all coefficients.
> - when dealing with nested loops, multiplication is used.

```c++
void algorithm(int n) {
    int a = 1; // zero operation or one operation
    a = a + n; // zero operation or one operation

    for (int i = 0; i < 5 * n + 1; i++) {// n operation or 5n + 1 operation
        cout << 0 << endl;
    }

//  n * n or (2n+1)*(n+1)
    for (int i = 0; i < 2 * n; i++) {// n operation or 2n +1 operation
        for (int j = 0; j < n + 1; j++) {
        // n operation or n+1 operation
            cout << 0 << endl;
        }
    }
}
```

`T(n) = 2(n+1)*(n+1) + 5n + 1 +2`

or

`T(n) = n^2 + n`

### Step two: determining the asymptotic upper bound.

The time complexity is determined by the highest-order term in the polynomial 𝑇(𝑛). This is because, as 𝑛 approaches infinity, the highest-order term will dominate, and the influence of other terms can be ignored.

| number of operation | time complexity |
| --- | --- |
| `100000` | `O(1)` |
| `3n+2` | `O(n)` |
| `2n^2 + 3n + 2` | `O(n^2)` |
| `n^3 + 10000n^2` | `O(n^3)` |
| `2^n + 10000n^2` | `O(2^n)` |

### Common Types

`𝑂(1) < 𝑂(log 𝑛) < 𝑂(𝑛) < 𝑂(𝑛 log 𝑛) < 𝑂(𝑛2) < 𝑂(2𝑛) < 𝑂(𝑛!)`

Constant Time Complexity < Logarithmic Time Complexity < Linear Time Complexity < Linear Logarithmic Time Complexity < Quadratic Time Complexity < Exponential Time Complexity < Factorial Time Complexity

## Space Complexity

the memory space used by an algorithm during its execution mainly includes the following types:

- input space: store the algorithm's input data.
- temporary space: store variables,objects,function context,and other data during he algorithm's runtime.
    - temporary data
    - stack frame space
    - instruction space
- output space: store the algorithm's output data.

```c++
struct Node {
    int val;
    Node *next;
    Node(int x) : val(x),next(nullptr) {}
};

int func() {
    return 0;
}

int algorithm(int n) { // input data
    const int a = 0; // temporary data
    int b = 0; // temporary data
    Node* node = new Node(0); // temporary data
    int c = func(); // stack frame space
    return a + b + c; // output data
}
```

we typically focus on the _worst-case_ space complexity.

- When considering the worst-case input data: when `𝑛 < 10`, the space complexity is `𝑂(1)`; however, when `𝑛 > 10`, the initialized array 'nums' occupies `𝑂(𝑛)` space. Therefore, the worst-case space complexity is `𝑂(𝑛)`.
- When considering the peak memory usage during algorithm execution: for instance, before executing the last line, the program occupies `𝑂(1)` space; when initializing the 'nums' array, the program occupies `𝑂(𝑛)` space. Hence, the worst-case space complexity is `𝑂(𝑛)`.
