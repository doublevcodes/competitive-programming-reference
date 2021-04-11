# Time Complexity

The **efficiency of algorithms** is important in competitive programming. Usually, it is easy to design an algorithm that solves the problem slowly, but the real challenge is to invent a **fast algorithm**. The time complexity of an algorithm estimates how much time the algorithm will use for some input. The idea is to represent the efficiency as a function whose parameter is the size of the input. By calculating the time complexity, we can find out whether the algorithm is fast enough **without implementing it**. Time complexity **does not tell you the running time of your algorithm** but merely estimates how the run time will increase as the size of an input to your algorithm increases.

## Big O Notation

The time complexity of an algorithm is denoted **O**(*···*) where the three dots represent some function.  Usually, the variable *n* denotes the **input size**.  For example, if the input is an array of numbers, *n* will be the size of the array, and if the input is a string, *n* will be the length of the string. The practice of denoting time complexities like this is often called **Big O Notation**

Here are a few examples of Big O Notation:

- **O**(*n*)
- **O**(log *n*)
- **O**(*n*²)

## Calculation rules

There are a few rules you can use to help you figure out the time complexity of a certain algorithm

### Loops

A common reason why an algorithm is slow is that it contains many loops that gothrough the input. The more nested loops the algorithm contains, the slower it is. If there are *k* nested loops, the time complexity is **O**(*nᵏ* ).

```cpp
for (int i = 0; i < n; i++) {
    /* Code goes here */
}
```

The time complexity of the above code is simply **O**(*n*). Whereas the time complexity of this code:

```cpp
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; i++) {
        /* Code goes here */
    }
}
```

is **O**(*n*²).

### Order of magnitude

The time complexity of an algorithm does not tell us the exact number of times the code inside a loop is executed, but it only shows the order of magnitude.  In the following examples, the code inside the loop is executed `3n`, `n+5` and `n/2` times, but the time complexity of each code is **O**(*n*)

```cpp
/* Code executed 3n times */
for (int i = 0; i < 3*n ; i++) {
    /* Code goes here */
}

/* Code executed n + 5 times */
for (int i = 0; i < n+5; i++) {
    /* Code goes here */
}

/* Code executed n/2 times */
for (int i = 1; i <= n; i += 2) {
    /* Code goes here */
}
```

As another example, the time complexity of the following code is **O**(*n*²):

```cpp
for (int i = 0; i < n; i++) {
    for (int j = i + 1; j < n; j++) {
        /* Code goes here */
    }
}
```

### Phases

If the algorithm consists of consecutive phases, the total time complexity is the largest time complexity of a single phase. The reason for this is that the slowest phase is usually the bottleneck of the code. For example, the following code consists of three phases with time complexities: **O**(*n*), **O**(*n*²) and **O**(*n*). Thus, the total time complexity is **O**(*n*²).

```cpp
/* Time complexity of O(n) */
for (int i = 0; i < n; i++) {
    /* Code goes here */
}

/* Time complexity of O(n^2) */
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        /* Code goes here */
    }
}

/* Time complexity of O(n) */
for (int i = 1; i <= n; i++) {
    /* Code goes here */
}
```

### Several variables

Sometimes the time complexity depends on several factors. In this case, the time complexity formula contains several variables.  For example, the time complexity of the following code is **O**(*nm*)

```cpp
for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) {
        /* Code goes here */
    }
}
```

### Recursion

The time complexity of a recursive function depends on the number of times the function is called and the time complexity of a single call.  The total time complexity is the product of these values. For example, consider the following function:

```cpp
void f(int n) {
    if (n == 1) {
        return;
    }
    f(n-1);
}
```

The call `f(n)` causes *n* function calls, and the time complexity of each call is **O**(*1*). Thus, the total time complexity is **O**(*n*). As another example, consider the following function:

```cpp
void g(int n) {
    if (n == 1) {
        return;
    }
    g(n-1);
    g(n-1);
}
```

In this case each function call generates two other calls, except for `n=1`. Let us see what happens when `g` is called with parameter `n`. The following table shows the function calls produced by this single call:
| Function call | Number of calls |
| --- | --- |
| g(n) | 1 |
| g(n−1) | 2 |
| g(n−2) | 4 |
| ··· | ··· |
| g(1) | 2ⁿ⁻¹ |

Based on this, the time complexity is

1 + 2 + 4 + ... + 2n − 1 = 2n − 1 = **O**(2*n*).
