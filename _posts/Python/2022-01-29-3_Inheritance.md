---
layout: single
title: "[Python] OOP: Inheritance"
categories: ["Python"]
tag: [oop, inheritance, python]
author_profile: true
sidebar_main: true
---

## `Inheritance`

Inheritance is the virtue of Object Oriented Programming. Python, of course, has one.

When you want to inherit a parent class, you put that parent class name in the parentheses of child class like `ChildClass(ParentClass)`. Notice that parent class's scope must contain the derive class definition.

You can change any number of classes but the `very base class` is `object` class. You don't have to explicity write `object` but you can see below that it works just fine.

The child class **inherits** all the `class attributes`. One of the main purposes of OOP is to avoid redundancy. Supose we have a parent class named `Person` and want to make a child class `Jason`.

TIP) One useful tip for inheritance is `IS TEST`. After you define a child class, ask yourself **is `child class` `parent class`?**. For the example below, `Is Jason (a) Person?` passes the IS TEST.

```python
class Person(object): # parent class
    def greeting(self):
        print("Hello")

class Jason(Person): # child class inheriting Person class
    pass


b = B()
b.greeting()
```

    Hello

Although we didn't specify any attributes for `Jason` class, it inherits `greeting` attribute so we can access it with the instance from `Jason` class.

### `Method overriding`

`Jason` class inherits `greeting` function object from `Person` class. However, Jason always says "what's up!" instead of "Hello". This is where **method overriding** kicks in. There are two rules you can remember for better understanding.

1. If an attribute is found in `child` class, access that.
2. If not, it keeps descending down to the inheritance until it finds the corresponding name(all the way down to `object` class).
3. If you define an attribute with the **exact same name** inheriting from somewhere down in the inheritance chain, the overrided attribute becomes active.

```python
class Person(object): # parent class
    def greeting(self):
        print("Hello")

class Jason(Person): # child class inheriting Person class
    def greeting(self):
        print("What's up!")


happy_jason = Jason()
happy_jason.greeting()
```

    What's up!

### Built-in functions for inheritance

- `isinstance()`: to check an instance's type: `isinstance(obj, type)` means **is `obj` an instance of `type`?**
- `issubclass()`: to check class inheritance: `issubclass(a,b)` means **is `a` a subclass of `b`?**

```python
class Person(object): # parent class
    def greeting(self):
        print("Hello")

class Jason(Person): # child class inheriting Person class
    def greeting(self):
        print("What's up!")


happy_jason = Jason()
print(isinstance(happy_jason, Jason)) # instance of Jason
print(isinstance(happy_jason, Person)) # instance of Person (inheritance)

print(issubclass(bool, int)) # bool is subclass of int, indeed. (inheritance)
print(issubclass(Jason, Person)) # Jason if subclassof Person  (inheritance)
```

    True
    True
    True
    True

### `super()`

`super()` enables you to interact with parent class. When initializing states, you can initialize the inherited attributes using `super().__init__(args)`.

This is in fact exactly the same as super(ChildClass, self).method(args).

the `self` refers to the `instance object` of the child class. So it's `super(Jason, self).__init__(name)`

```python
class Person():
    def __init__(self, name):
        self.name = name

    def greeting(self):
        print("Hello")

class Jason(Person):
    def __init__(self, name):
        super().__init__(name) # call Person's __init__ method with argument "name"
        # super(Jason,self).__init__(name) # same as above

    def greeting(self):
        print("What's up")
```

```python
j = Jason("Jason")

print(j.name)
j.greeting()
```

    Jason
    What's up

Great job! Now you have learned how inheritance is and how to initialize child class's instance object using `super()`. For more information, refer to

- [freecodeacademy](https://docs.python.org/3/tutorial/classes.html)

- [documentation](https://docs.python.org/3/tutorial/classes.html)

```python

```
