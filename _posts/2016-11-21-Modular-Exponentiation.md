---
layout: post
title: Modular Exponentiation
date: 2016-11-20 12:00
excerpt: What is the fastest way to compute a large integer power of a number modulo m?
tags: [ACM-ICPC, Competitive Programming, Algorithms]
comments : true
---

![modExpo](/assets/img/algo-image/modExpo/mod-expo.jpg)

What is the fastest way to compute a large integer power of a number modulo m?

Sometimes, we need to calculate reminder of a number raised to an integer power.  

$$x^y \mod m$$

One way to do this is iteratively multiply the base and take reminder with mod at each step. 

```cpp
int modExpo (int x, int y, int m) {
    long long result = 1;
    for (int i=0; i < y; i++) {
        result = (result * x) % m;
    return result;
}
```

However, this algorithm is performing in linear time, $$O(y)$$. So, for really large powers, performance would be fairly slow.  

We can reduce time complexity to $$O(\log_2{y})$$ by using what is called as exponentiation by squaring. 


### Exponentiation by squaring

Basic idea of exponentiation by squaring is

![expo-by-square](/assets/img/algo-image/modExpo/expo-by-square.png)


If power is 0, algorithm should return 1. It is the base case, other cases will built on it.  

Other than it, at each step we are dividing the exponent by two and square the base, and then for the case where the exponent is odd you multiply the result by the base. 

At each step we pretty much cut the problem in half, adding an extra multiplication for odd numbers. So, complexity of algorithm become $$O(\log_2{y})$$.


You can implement algorithm in two ways, recursively or iteratively.


#### Recursive Version

```cpp
long long modExpo (int x, int y, int m) {
    if (y == 0)
        return 1;
    else if (y%2 == 0) 
        return modExpo (x*x, y/2, m) % m;
    else 
        return ((x%m) * modExpo (x*x, (y-1)/2, m)) % m;
}
```

Recursive version is relatively slow, so iterative version is recommended.

#### Iterative Version

```cpp
long long modExpo (int x, int y, int m) {
    if (y == 0)
        return 1;

    long long res = 1;
    x = x % m;
    while (y > 0) {
        if (y%2 == 0) { 
            x = (x * x) % m;
            y = y/2;
        }
        else {
            res = (res * x) % m
            x = (x * x) % m; 
            y = y/2;
       }
    }
    return res;
}
```

And here’s the most optimized iterative version:

```cpp
long long modExpo (int x, int y, int m) {
    if (y == 0)
        return 1;

    x = x % m;
    long long res = 1;
    while (y > 0) {
        if (y%2)
            res = (res * x) % m;
        x = (x * x) % m; 
        y = y/2;
    }
    return res;
}
```


#### Tip:

At most of the competitive programming questions ask to output for large number as modulo $$10^9+7$$. Why?
You can check [this quora question](https://www.quora.com/What-exactly-is-print-it-modulo-10-9-+-7-in-competitive-programming-websites) for answer.
