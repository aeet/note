---
title: "Summary of 《Hello, Algorithm》- 06"
date: "2023-12-18"
categories: 
  - "algorithm"
  - "hello-algorithm"
tags: 
  - "algorithm"
coverImage: "9113d84e4dfc4d5997fde48d69c96ec7.jpg"
---

# hash algorithm

## intro

- Whether it is open addressing or chain addressing, they can only ensure that the hash table works normally when a collision occurs, but cannot reduce the occurrence of hash collisions
- If hash collisions occur too frequently, the performance of the hash table will deteriorate rapidly.
- In the ideal case, key-value pairs are evenly distributed in each bucket, achieving the best query efficiency.
- In the worst case, all key-value pairs are stored in the same bucket, and the time complexity degrades to `O(n)`
- The distribution of key-value pairs is determined by the hash function.

* * *

- The hash algorithm should contain the following characteristics.
    - Determinism: For the same input, a hashing algorithm should always produce the same output.
    - High efficiency: The process of calculating hash values should be fast enough. The smaller the computational overhead, the higher the practicality of the hash table.
    - Uniform distribution: The hash algorithm should make the key-value pairs evenly distributed in the hash table. The more even the distribution, the lower the probability of hash collisions.

* * *

- Hash algorithms used in other fields
    - Password storage
    - Data integrity check

* * *

- Characteristic:
    - One-way: No infomation about the input data can be deduced form the hash value.
    - Collision resistance: It should be extremely difficult to find two different inputs such that their hash values are the same.
    - Avalanche effect: Small changes in input should lead to significant and unpredictable changes in output.

## hash algorithm design

- Additive hashing: Add the ASCII codes of each character entered and use the resulting sum as the hash value.
- Multiplicative hasing: Taking advantage of the irrelevance of mutiplicaiton, each round is multiplied by a constant to accumulate the ASCII code of each charater into the hash value.
- XOR Hash: Eeach element of the input data is accumulated in to a hash value through the XOR operation.
- Rotated hashing: Accumulate the ASCII code of each character into a hash value, and rotate the hash value before each accumulation.

```cpp
// Additive hashing
int addHashing(string key){
    long long hash = 0;
    const int MODULUS = 1000000007;
    for(unsigned char c:key){
        hash = (hash + (int)c)&MODULUS;
    }
    return (int) hash;
}

// Multiplicative hashing
int mulHash(string key) {
    long long hash = 0;
    const int MODULUS = 1000000007;
    for (unsigned char c : key) {
        hash = (31 * hash + (int)c) % MODULUS;
    }
    return (int)hash;
}

// XOR hashing
int xorHash(string key) {
    int hash = 0;
    const int MODULUS = 1000000007;
    for (unsigned char c : key) {
        // XOR
        hash ^= (int)c;
    }
    return hash & MODULUS;
}

// Rotated hashing
int rotHash(string key){
    long long hash = 0;
    const int MODULUS = 1000000007;
    for(unsigned char c:key){
        hash = ((hash << 4) ^ (hash >>28) ^ (int)c)%MODULUS;
    }
    return (int) hash;
}
```

- When we use large prime numbers as the modulus, we can maximize the uniform distribution of hash values. Because the prime numbers do not differ from other numbers. The existence of common denominators for words can reduce periodic patterns caused by modulo operations and thus avoid hash collisions.

```
modulus =   9;
key = {0,3,6,9,12,15,18,21,24,27,30,33,....}
hash= {0,3,6,0,3,6,0,3,6,0,3,6......}
```

The hash value will be piled up, thus aggravating the hash conflict.

* * *

```
modulus = 13
key = {0,3,6,9,12,15,18,21,24,27,30,33,....}
hash = {0,3,6,9,12,2,5,8,11,1,4,7}
```

- We usually choose a prime number as the modulus, and this prime number should be large enough to eliminate periodic patterns as much as possible and improve hashing operations soundness of law.

* * *

Common hashing algorithms

|  | MD5 | SHA-1 | SHA-2 | SHA-3 |
| --- | --- | --- | --- | --- |
| at launch between | 1992 | 1995 | 2002 | 2008 |
| output long spend | 128bits | 160bits | 256/512bits | 224/256/384/512bits |
| hash rush sudden | S | S | C | C |
| safety etc. class | C | C | S | S |
| apply | deprecated | deprecated | cryptocurrency transaction verification, numbers signature etc | can be used as an alternative to SHA‑2 |
