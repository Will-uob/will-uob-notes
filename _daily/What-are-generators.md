---
published: true
date: 07-09-2023
title: What are generators?
tags: Python Programming
---

# What are generators?
We've already mentioned what list comprehensions are in the <a class="wiki-link" href="/daily/Greatest-common-divisor-of-strings">greatest common divisor of strings</a> article, but now I think it's a good
time to mention generators.

A generator expression is similar to a list comprehension, with the exception that it doesn't construct
a ```List``` object. Instead of creating a list and storing it in memory, it only creates the next
element in demand.

When a normal function with a return statement is called, it terminates whenever it gets a return
statement. But a function with a yield statement saves the state of the function, which can be
picked up from that state on the next call. (I... didn't know Python could do that UwU).

### How do you create and interact with generators?
An example expression is as follows:
```
generator_expression = (i for i in range(11) if i % 2 == 0)
print(generator_expression) # <generator object at 0x000001452B1EEC50>
```

In this example, if we want to print the output for generator expressions, we can iterate it over
the generator object.

```
for i in generator_expression:
    print(i, end=" ")
```

What's the purpose of using generator expressions? They are far more memory efficient that using
lists, since the entire list isn't stored in memory. (Once again, this seems awfully similar to
Haskell...)
