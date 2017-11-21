---
layout: post
title:  "從 javascript 看 python"
date:   2016-05-04 14:30:00 +0800
categories: Python
---

  學習 [Python][1] 筆記，紀錄與 javascript 語法特別的地方．(不完整版)

## The range() Function
```sh
>>> a = ['Mary', 'had', 'a', 'little', 'lamb']
>>> for i in range(len(a)):
...     print i, a[i]
...
0 Mary
1 had
2 a
3 little
4 lamb
```

## break and continue Statements, and else Clauses on Loops
```sh
>>> for n in range(2, 10):
...     for x in range(2, n):
...         if n % x == 0:
...             print n, 'equals', x, '*', n/x
...             break
...     else:
...         # loop fell through without finding a factor
...         print n, 'is a prime number'
...
2 is a prime number
3 is a prime number
4 equals 2 * 2
5 is a prime number
6 equals 2 * 3
7 is a prime number
8 equals 2 * 4
9 equals 3 * 3
```
```sh
>>> for num in range(2, 10):
...     if num % 2 == 0:
...         print "Found an even number", num
...         continue
...     print "Found a number", num
Found an even number 2
Found a number 3
Found an even number 4
Found a number 5
Found an even number 6
Found a number 7
Found an even number 8
Found a number 9
```

## pass Statements
```sh
>>> while True:
...     pass  # Busy-wait for keyboard interrupt (Ctrl+C)
...
```
```sh
>>> class MyEmptyClass:
...     pass
...
```
```sh
>>> def initlog(*args):
...     pass   # Remember to implement this!
...
```

## The default value is evaluated only once.
```sh
def f(a, L=[]):
    L.append(a)
    return L

print f(1)
print f(2)
print f(3)
```
```sh
def f(a, L=None):
    if L is None:
        L = []
    L.append(a)
    return L
```

## Keyword Arguments
```sh
def cheeseshop(kind, *arguments, **keywords):
    print "-- Do you have any", kind, "?"
    print "-- I'm sorry, we're all out of", kind
    for arg in arguments:
        print arg
    print "-" * 40
    keys = sorted(keywords.keys())
    for kw in keys:
        print kw, ":", keywords[kw]
```

## Lambda Expressions
```sh
>>> def make_incrementor(n):
...     return lambda x: x + n
...
>>> f = make_incrementor(42)
>>> f(0)
42
>>> f(1)
43
```

[1]:https://www.python.org/
