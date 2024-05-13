---
title: "Log"
date: "2023-11-14"
categories: 
  - "basic"
  - "mathematics"
tags: 
  - "math"
coverImage: "2300973acccb48c5920aa552179cb944-scaled.jpg"
---

# Intro

- In mathematics, a logarithm `log` is a mathematical function that describes the exponent to which a fixed number, called the base, must be raised to obtain a certain number.
- There are two common logarithms:
    - the natural logarithm `ln`, which has the base `e` (approximately 2.71828).
    - the common logarithm `log`, which has the base `10`.
- Natural Logarithm `ln`: If we denote the natural logarithm as `ln(x)`, it represents the power to which `e` must be raised to equal `x`.
    - example `ln(e) = 1`, because `e` to the power of `1` equals `e`
- Commn Logarithm `log`: If we denote the common logarithm as `log(x)`, it represents the power of which 10 must be raised to qual `x`.
    - example `log(100) = 2`, because `10^2 = 100`.

```katex
log_a(b) = c
```

- `a` is the base.
- `b` is the argument or the number for which we are finding the logarithm.
- the equation can be read as "the logarithm base `a` of `b` is equal `c`"

# Properties

- Define Propertie: If `a^b = c`,then `log_a(c) = b`.This property expresses the logarithm as the inverse operation of exponentiation.
- Base Change Formula: `log_a(b) = \frac{log_c(b)}{log_c(a)}` where `c` is a postive number not equal to 1.This formula allows the conversion of logarithms between different bases.
- Multiplication Property: `log_a(bc) = log_a(b) + log_a(c)`. This property states that the logarithm of a product is the sum of the logarithms.
- Divison Property:`log_a(\frac{b}{c}) = log_a(b) - log_a(c)`. This property indicates that the logarithm of a quotient is the difference of the logarithms.
- Power Property: `log_a(b^n) = n log_a(b)`.This property allows the exponent in a logarithmic expression to be moved to the front.
