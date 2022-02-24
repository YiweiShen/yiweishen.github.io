title: random Module
date: 2017-04-03 20:27:00
tags: python
---
First of all, in Python 3
```python
import random
```
You would find the documentation on page of
https://docs.python.org/3/library/random.html
in which it said that almost all module functions depend on the basic function random(), which generates a random float uniformly in the semi-open range [0.0, 1.0).

Normally I would not talk about the deeper side of the module such as the core generator.  However in this case, you have to know that Python uses the Mersenne Twister as the core generator.

It produces 53-bit precision floats and has a period of 2**19937-1. The underlying implementation in C is both fast and threadsafe. The Mersenne Twister is one of the most extensively tested random number generators in existence. However, being completely deterministic, it is not suitable for all purposes, and is completely unsuitable for cryptographic purposes.

I say it again that random Module is unsuitable for cryptographic purposes.  Other than that you could use it all the time.
```python
random.random() # 0.01658182124355423
random.uniform(1.5, 100.5) # 17.133710707896064
random.seed(1) # seeding, otherwise, the current time is used
random.randint(1, 100) # Random Integers
random.randint(-5, 5)
random.randint(a, b) # Return a random integer N such that a <= N <= b
random.randrange(0, 101, 5)
random.choice('abc')
random.choices(['red', 'black', 'green'], [18, 18, 2], k=6) # ['red', 'green', 'black', 'black', 'red', 'black']
words =['a','b','c','d']
random.shuffle(words) # ['d', 'b', 'a', 'c']
random.sample('abcdefg',2) # ['f', 'a']
```
By the way, for security or cryptographic uses, there is a module called secrets.