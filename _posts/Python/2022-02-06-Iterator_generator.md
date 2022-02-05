---
layout: single
title: "[Python] What really is the iterator and generator?"
categories: ["Python"]
tag: [iterator, generator, python]
author_profile: true
sidebar_main: true
---

> # Iterable

An **iterable** is any object that has `__iter__` or `__getitem__` method which returns an **iterator** or can take indices. In other words, python objects are **iterable** if we can get an **iterator** from them.

- list, dict, set, str, bytes, tuple, range (iterable container)

```python
dir(range)[5:20]
```

    ['__doc__',
     '__eq__',
     '__format__',
     '__ge__',
     '__getattribute__',
     '__getitem__',
     '__gt__',
     '__hash__',
     '__init__',
     '__init_subclass__',
     '__iter__',
     '__le__',
     '__len__',
     '__lt__',
     '__ne__']

> # Iterator

An iterator is any object that has `__next__` method and `__iter__` method that returns itself. These two magic methods are known together as **iterator protocol**. In order to get the **iterator** from an **iterable** object, you can call the `__iter__` function by either

1. `container.__iter__()`
2. `iter(container)`

where `iter()` is a built-in function (see [built-in functions](https://docs.python.org/3/library/functions.html#iter)) that returns an iterator object.

```python
lst_iterable = [1,2,3,4] # an iterable container
lst_iterator1 = lst_iterable.__iter__()
lst_iterator2 = iter(lst_iterable)
print(lst_iterator1)
print(lst_iterator2)
```

    <list_iterator object at 0x7f988d649160>
    <list_iterator object at 0x7f988d95c460>

> ## `next()` or `.__next__()` function

The important thing about **iterator** is that it has `__next__` function that returns the next item from the iterator. Each time you call the `?.__next__()` or `next(?)` where ? is an iterator, then it tosses you the next element starting from the beginning of the original iterable container. It remembers the last element that was pulled out, so each time you call `next()`, you're reaching to the end of the container. Of course, if you go **beyond** the limit, it will raise the `StopIteration` error. You can return set the default value instead of returning StopIteration error. Let's see in code.

```python
lst_iterable = [1,2,3,4] # "iterable"
lst_iterator = iter(lst_iterable) # "iterator"
print(next(lst_iterator))
print(next(lst_iterator))
print(next(lst_iterator))
print(next(lst_iterator))
print(next(lst_iterator))
```

    1
    2
    3
    4



    ---------------------------------------------------------------------------

    StopIteration                             Traceback (most recent call last)

    Input In [60], in <module>
          5 print(next(lst_iterator))
          6 print(next(lst_iterator))
    ----> 7 print(next(lst_iterator))


    StopIteration:

You see that the 5th `next()` call indeed raises the `StopIteration` call since all the items are exhausted. If you pass the second parameter to `next(iterator, default)`, then it will return the passed value instead of raising an exception.=

```python
lst_iterable = [1,2,3,4] # "iterable"
lst_iterator = iter(lst_iterable) # "iterator"
print(next(lst_iterator))
print(next(lst_iterator))
print(next(lst_iterator))
print(next(lst_iterator))
print(next(lst_iterator, "Don't even think about that"))
```

    1
    2
    3
    4
    Don't even think about that

> ## The hidden secret of `for loop`

We all are too good at for loop. It's a basic building block of any code. But what is actually happening behind the hood? What really happens if we run a `for loop`? The answer is in the `iterator`. Below is the basic for loop.

```python
lst = [1,2,3,4] # iterable o, iterator x

for element in lst:
    ########Loop Body#######
    print(element, end=" ")
    ########Loop Body#######
```

    1 2 3 4

What's really happening behind the hood is that `for loop` creates an `iterable` from the `iterable` container and run `infinite white loop` until all the elements are exhausted. Let's see what it means.

```python
# Above for loop is equal to..
lst_iterator = iter(lst)

while True:
    try:
        element = next(lst_iterator)
        ########Loop Body#######
        print(element, end=" ")
        ########Loop Body#######
    except StopIteration:
        break
```

    1 2 3 4

> ## sentinel in `iter()`

`iter()` can have an additional second argument called **sentinel**. If you provide the sentinel, then the first argument must be a **callable object**. Then, the iterator will call the object with no arguments until the returned value is equal to the sentinel.

```python
def return_year():
    return "2023"

my_iterator = iter(return_year, "2023")
print(next(my_iterator))
print(next(my_iterator))
print(next(my_iterator))
print(next(my_iterator))
print(next(my_iterator))
```

    ---------------------------------------------------------------------------

    StopIteration                             Traceback (most recent call last)

    Input In [3], in <module>
          2     return "2023"
          4 my_iterator = iter(return_year, "2023")
    ----> 5 print(next(my_iterator))
          6 print(next(my_iterator))
          7 print(next(my_iterator))


    StopIteration:

In above case, since `next(my_iterator)` will call the `return_year` function but "2022" never equals "2023" so it will only print "2022." One useful application of the sentinel is **block-reader** of a file.

> # Building custom iterator

It's of course possible to build our own `iterator`! But don't forget you have to implement `__next__` and `__iter__` functions where `__next__` returns the next item and `__iter__` returns the iterator object itself.

```python
class raised_two:
    def __init__(self, limit=0):
        self.limit = limit

    def __iter__(self):
        self.n = 1
        return self # Remember: must return the iterator object itself

    def __next__(self):
        if self.n <= self.limit: # if not exhausted,
            result = self.n ** 2
            self.n += 1
            return result # return the next element
        else: # if exhausted,
            raise StopIteration # raise StopIteration exception


sequence = raised_two(5) # create an object
i = iter(sequence) # create an iterator from the object
print(next(i))
print(next(i))
print(next(i))
print(next(i))
print(next(i))
print(next(i))
```

    1
    4
    9
    16
    25



    ---------------------------------------------------------------------------

    StopIteration                             Traceback (most recent call last)

    Input In [98], in <module>
         23 print(next(i))
         24 print(next(i))
    ---> 25 print(next(i))


    Input In [98], in raised_two.__next__(self)
         13     return result # return the next element
         14 else: # if exhausted,
    ---> 15     raise StopIteration


    StopIteration:

> # Generator

In above, we made our custom iterator. But, that's a bit lengthy and unhealthy. Is there any better way to make an iterator? Then generator the go-to.

In short, a generator is a **iterator maker**. A **function** automatically becomes a **generator** function if it has at least one `yield` statement and optionally `return` statements. The difference between `return` and `yield` in a generator is that the `return` statement entirely terminates the function while the `yield` statement **pauses the function with all the states saved and later continues from that breakpoint**. Below are couple rules of generator. Then, when you call `next()` function, the generator **resumes where it left off with all the data remembered and lastly executed line**

(NOTE) I find it a bit confusing for the fact that `generator` itself is not the `generator function`. In below, `my_gen` is just a normal (generator) function but when you call it `my_gen()`, it returns the `generator`. So in my understanding, generators casually refer to the (generator) functions and generators are just like iterators.

1. When a generator function is **called**, it returns an **iterator** (or generator) but does not immediately execute the function body.
2. `__iter__` and `__next__` are automatically implemented. So we can use `next()`.
3. You can do anything for generator that you can do with class-based iterators.
4. Once the generator function `yields`, it **pauses** the execution and the control is **transferred** to the caller (this statement is referenced from Programiz)
5. All the local variables and location of last execution are remembered.
6. When the generator function is terminated, then `StopIteration` exception will be automatically raised.

```python
def my_gen(): # generator function
    a = 10
    yield 1 # step 2 - pause
    yield 2 # step 4 - pause
    yield 3 # step 6 - pause

print(f"my_gen type: {my_gen}")
print(f"my_gen() type: {my_gen()}")

gen_iterator = my_gen() # returns a generator
print(next(gen_iterator)) # step 1
print(next(gen_iterator)) # step 3
print(next(gen_iterator)) # step 5
print(next(gen_iterator)) # step 7
```

    my_gen type: <function my_gen at 0x7f988e3c28b0>
    my_gen() type: <generator object my_gen at 0x7f988e453ac0>
    1
    2
    3



    ---------------------------------------------------------------------------

    StopIteration                             Traceback (most recent call last)

    Input In [120], in <module>
         11 print(next(gen_iterator)) # step 3
         12 print(next(gen_iterator)) # step 5
    ---> 13 print(next(gen_iterator))


    StopIteration:

```python
def my_gen(): # generator function
    yield 1 # step 2 - pause
    yield 2 # step 4 - pause
    yield 3 # step 6 - pause

print(f"my_gen type: {my_gen}")
print(f"my_gen() type: {my_gen()}")

gen_iterator = my_gen() # returns a generator
print(next(gen_iterator)) # step 1
print(next(gen_iterator)) # step 3
print(next(gen_iterator)) # step 5
print(next(gen_iterator)) # step 7
```

    my_gen type: <function my_gen at 0x7fd1cb84a1f0>
    my_gen() type: <generator object my_gen at 0x7fd1cb82dba0>
    10
    10
    10



    ---------------------------------------------------------------------------

    StopIteration                             Traceback (most recent call last)

    Input In [4], in <module>
         12 print(next(gen_iterator)) # step 3
         13 print(next(gen_iterator)) # step 5
    ---> 14 print(next(gen_iterator))


    StopIteration:

Since a generator is just like any other iterator, we can use for loop directly.

```python
for ele in my_gen():
    print(ele)
```

    10
    10
    10

> # Generator Expressions

Similar to list comprehensions, you can simply and succintly create generators using **generator expressions**. Instead of square-brackets in list comprehensions, use **parentheses** instead.

```python
generator = (x*x for x in range(1,10))
print(generator)
```

    <generator object <genexpr> at 0x7fd1cb82dba0>

Now we can do whatever we want to with a generator!

```python
print(next(generator))
print(next(generator))
print(next(generator))
print(next(generator))
print(next(generator))
```

    1
    4
    9
    16
    25

> # Why Generators?

## 1. Memory Efficient

Consider a normal function returns a sequence of **100 million** numbers which seems horrible to the memory. However, a generator does not allocate memory to all the elements at the same time.

## 2. Can handle infinite streams

```python
def infinite_series():
    n = 0
    while True:
        yield n
        n += 1
```
