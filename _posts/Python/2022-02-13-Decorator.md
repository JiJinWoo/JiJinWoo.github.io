---
layout: single
title: "[Python] Decorator"
categories: ["Python"]
tag: [decorator]
author_profile: true
sidebar_main: true
---

> # Decorator

**Decorator** in Python a function that takes another function and returns it with additional functionalities (decorate).

Before understanding decorator, you need to understand two concepts: **first class function** and **closure**.

> ## First class function

Remember everything in Python is an **object**, even class or function. In other words, you can assign a function to a variable, pass a function as an argument. Let's see with examples.

## Assign a function to a variable

```python
def greeting():
    print("hello")

func = greeting
func()
```

    hello

As you can see, you can assign a function to a variable just like you assign any other variable.

## Pass a function as an argument

```python
def greeting(func):
    func()

def say_hello():
    print("Hello")

greeting(say_hello)
```

    Hello

You can also pass a function as an argument to another function. So everything in Python is really an object!

> ## Closure

Closure is an interesting concept. Let's first understand what **nested function** and **nonlocal variable** are. A nested function is literally a function nested in another function like `inner()` in the example below. Nonlocal variable is a variable outside the current namespace. `x` is the nonlocal variable for `inner()`.

Now let's see what a closure looks like.

```python
def outer():
    x = 10 # nonlocal var for inner()
    def inner():
        print(x)
    return inner

func = outer() # outer() execution is finished at this point
del outer
func() # but still can access nonlocal variable x
```

    10

You see that `inner()` function is nested inside `outer()` function which has `x` variable. After executing `func = outer()`, `inner` function is assigned to `func`. At this point, `outer()` function is done being executed so its namespace should be removed. However, when we call `func()`, `inner()` can **still access** the nonlocal variable `x`.

The nonlocal variables are **remembered** even after the outer function is executed or the function itself is deleted out of namespace. This technique is called **closure** in Python.

## Criteria of Closure

To create closures, three criteria must be met.

1. Must have a nested function (`inner`)
2. The enclosing function(`outer`) must return the nested function(`inner`)
3. The nested function must refer to a nonlocal variable in the enclosing function (`x`)

> ## Closure Example

```python
def make_raised_to_power_of(k):
    def power_of(x):
        return x ** k
    return power_of

power2 = make_raised_to_power_of(2)
power3 = make_raised_to_power_of(3)
power5 = make_raised_to_power_of(5)

print(power2(5))
print(power3(5))
print(power5(5))
```

    25
    125
    3125

```python
def make_tag(tag_name):
    def tag_func(msg):
        return "<"+tag_name+">" + msg + "</" + tag_name + ">"
    return tag_func

h1_tag_func = make_tag('h1')
print(h1_tag_func("hello"))
```

    <h1>hello</h1>

> # Decorator

As mentioned earlier, a decorator takes in a function, decorates, and returns it. Let's look at an example.

```python
def my_name_is():
    print("My name is Jason")

my_name_is()
```

    My name is Jason

Suppose we have a function `my_name_is` which prints "My name is Jason".

When you call it, of course, it prints "My name is Jason". But isn't that a bit boring? We want to add some decorations.

```python
def decorator_func(func):
    def inner():
        print("Hello,")
        func()
        print("Best luck.")
    return inner

def my_name_is():
    print("My name is Jason")

my_name_is = decorator_func(my_name_is)
my_name_is()
```

    Hello,
    My name is Jason
    Best luck.

We passed `my_name_is` to `decorator_func` and returned the `inner` function which again calls the original `my_name_is` with some extra functionalities. This is what decorator does. But, it's a bit annoying to write `my_name_is = decorator_func(my_name_is)` everytime. So we instead use decorator symbol `@`.

The above example is equivalent to below.

```python
def decorator_func(func):
    def inner():
        print("Hello,")
        func()
        print("Best luck.")
    return inner

@decorator_func
def my_name_is():
    print("My name is Jason")

my_name_is()
```

    Hello,
    My name is Jason
    Best luck.

Look! They both gave the same results. `@decorator_func` does the exact same thing as `my_name_is = decorator_func(my_name_is)`.

> ## `@classmethod`

`classmethod()` function transforms a function to a **class method** which you can call with `ClassName.method()`. A classmethod must contain the first parameter, by convention, `cls`. `@classmethod` is a built-in decorator which does the same job as `classmethod()`.

```python
class Person(object):
    def non_class_method(self):
        print("This is non-class method")

    @classmethod
    def class_method(cls):
        print("This is class method")

Person.class_method() # This is actually equivalent to Person.class_method(Person)
```

    This is class method

```python
Person.non_class_method()
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-8-83121106f096> in <module>
    ----> 1 Person.non_class_method()


    TypeError: non_class_method() missing 1 required positional argument: 'self'

If you call non-class method using class name, it will throw an exception.

> ## `@staticmethod`

Similar to `@classmethod`, `@staticmethod` is a built-in decorator that defines a static method which you can call either by an **instance** or **class**. The difference between the classmethod is that a static method does not require the first parameter.

```python
class Person(object):
    def non_static_method(self):
        print("This is non-static method")

    @staticmethod
    def static_method():
        print("This is static method")

Person.static_method()
```

    This is static method

> ## `@property`

`@property` is a built-in decorator for `property()` function. When `@property` is used, the method becomes a property. Let's look at an example.

```python
class Person(object):
    def __init__(self, name):
        self.__name = name

    @property
    def name(self):
        return self.__name

p1 = Person("Jason")
print(p1.name)
```

    Jason

With `@property`, you can use the method name just like any other member variable. However, note that it's only possible to **access** it but cannot modify it. Look below,

```python
class Person(object):
    def __init__(self, name):
        self.__name = name

    @property
    def name(self):
        return self.__name

p1 = Person("Jason")
p1.name = "Jacob"
```

    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-31-68e1b869f7ef> in <module>
          8
          9 p1 = Person("Jason")
    ---> 10 p1.name = "Jacob"


    AttributeError: can't set attribute

> ### `@propertyname.setter`

If you want to modify the property defined with `@property`, then you can overload the method with `@<propertyname>.setter`.

```python
class Person(object):
    def __init__(self, name):
        self.__name = name

    @property
    def name(self):
        return self.__name

    @name.setter
    def name(self, value):
        self.__name = value

p1 = Person("Jason")
p1.name = "Jacob"
print(p1.name)
```

    Jacob

See that with `@name.setter`, you can now modify the property the same you for other regular member variables.

> ### `@propertyname.deleter`

Just like setter, you can have `@propertyname.deleter` decorator to enable deletion of the property.

```python
class Person(object):
    def __init__(self, name):
        self.__name = name

    @property
    def name(self):
        return self.__name

    @name.setter
    def name(self, value):
        self.__name = value

    @name.deleter
    def name(self):
        del self.__name

p1 = Person("Jason")
p1.name = "Jacob"

print(p1.name)
del p1.name
print(p1.name)
```

    Jacob



    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-46-ce555be4aacd> in <module>
         20 print(p1.name)
         21 del p1.name
    ---> 22 print(p1.name)


    <ipython-input-46-ce555be4aacd> in name(self)
          5     @property
          6     def name(self):
    ----> 7         return self.__name
          8
          9     @name.setter


    AttributeError: 'Person' object has no attribute '_Person__name'

See now you successfully deleted the property so you get an error when you access it again.

```python

```
