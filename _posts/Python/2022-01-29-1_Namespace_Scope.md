---
layout: single
title: "[Python] Namespace and Scope"
categories: ["Python"]
tag: [namepsace, scope, python]
author_profile: true
sidebar_main: true
---

## `Namespace`

We've been hearing about the word `namespace` all the time. But what the heck is it really??

- A `namespace` is a mapping from `names` to `objects`. In python, namespaces are internally implemented as `dictionary`. The following are the examples of namespace
  - `built-in` namespace
  - `global` namespace $($same as module namespace$)$
  - `local` namespace
- It's worth mentioning that `global` namespace is **writable** which mean you can modify it. However, you **cannot** modify the `local` namespace.

### `built-in` namespace

The module `import builtins` gives us direct access to all 'built-in identifiers such as `open()`, `__name__`, `__doc__`, `all()`, `any()`, `abs()`, all the `exceptions`and other built-in identifiers you've seen out there!

```python
import builtins
builtins.__dict__
```

    {'__name__': 'builtins',
     '__doc__': "Built-in functions, exceptions, and other objects.\n\nNoteworthy: None is the `nil' object; Ellipsis represents `...' in slices.",
     '__package__': '',
     '__loader__': _frozen_importlib.BuiltinImporter,
     '__spec__': ModuleSpec(name='builtins', loader=<class '_frozen_importlib.BuiltinImporter'>, origin='built-in'),
     '__build_class__': <function __build_class__>,
     '__import__': <function __import__>,
     'abs': <function abs(x, /)>,
     'all': <function all(iterable, /)>,
     'any': <function any(iterable, /)>,
     'ascii': <function ascii(obj, /)>,
     'bin': <function bin(number, /)>,
     'breakpoint': <function breakpoint>,
     'callable': <function callable(obj, /)>,
     'chr': <function chr(i, /)>,
     'compile': <function compile(source, filename, mode, flags=0, dont_inherit=False, optimize=-1, *, _feature_version=-1)>,
     'delattr': <function delattr(obj, name, /)>,
     'dir': <function dir>,
     'divmod': <function divmod(x, y, /)>,
     'eval': <function eval(source, globals=None, locals=None, /)>,
     'exec': <function exec(source, globals=None, locals=None, /)>,
     'format': <function format(value, format_spec='', /)>,
     'getattr': <function getattr>,
     'globals': <function globals()>,
     'hasattr': <function hasattr(obj, name, /)>,
     'hash': <function hash(obj, /)>,
     'hex': <function hex(number, /)>,
     'id': <function id(obj, /)>,
     'input': <bound method Kernel.raw_input of <ipykernel.ipkernel.IPythonKernel object at 0x7fd68043b790>>,
     'isinstance': <function isinstance(obj, class_or_tuple, /)>,
     'issubclass': <function issubclass(cls, class_or_tuple, /)>,
     'iter': <function iter>,
     'len': <function len(obj, /)>,
     'locals': <function locals()>,
     'max': <function max>,
     'min': <function min>,
     'next': <function next>,
     'oct': <function oct(number, /)>,
     'ord': <function ord(c, /)>,
     'pow': <function pow(base, exp, mod=None)>,
     'print': <function print>,
     'repr': <function repr(obj, /)>,
     'round': <function round(number, ndigits=None)>,
     'setattr': <function setattr(obj, name, value, /)>,
     'sorted': <function sorted(iterable, /, *, key=None, reverse=False)>,
     'sum': <function sum(iterable, /, start=0)>,
     'vars': <function vars>,
     'None': None,
     'Ellipsis': Ellipsis,
     'NotImplemented': NotImplemented,
     'False': False,
     'True': True,
     'bool': bool,
     'memoryview': memoryview,
     'bytearray': bytearray,
     'bytes': bytes,
     'classmethod': classmethod,
     'complex': complex,
     'dict': dict,
     'enumerate': enumerate,
     'filter': filter,
     'float': float,
     'frozenset': frozenset,
     'property': property,
     'int': int,
     'list': list,
     'map': map,
     'object': object,
     'range': range,
     'reversed': reversed,
     'set': set,
     'slice': slice,
     'staticmethod': staticmethod,
     'str': str,
     'super': super,
     'tuple': tuple,
     'type': type,
     'zip': zip,
     '__debug__': True,
     'BaseException': BaseException,
     'Exception': Exception,
     'TypeError': TypeError,
     'StopAsyncIteration': StopAsyncIteration,
     'StopIteration': StopIteration,
     'GeneratorExit': GeneratorExit,
     'SystemExit': SystemExit,
     'KeyboardInterrupt': KeyboardInterrupt,
     'ImportError': ImportError,
     'ModuleNotFoundError': ModuleNotFoundError,
     'OSError': OSError,
     'EnvironmentError': OSError,
     'IOError': OSError,
     'EOFError': EOFError,
     'RuntimeError': RuntimeError,
     'RecursionError': RecursionError,
     'NotImplementedError': NotImplementedError,
     'NameError': NameError,
     'UnboundLocalError': UnboundLocalError,
     'AttributeError': AttributeError,
     'SyntaxError': SyntaxError,
     'IndentationError': IndentationError,
     'TabError': TabError,
     'LookupError': LookupError,
     'IndexError': IndexError,
     'KeyError': KeyError,
     'ValueError': ValueError,
     'UnicodeError': UnicodeError,
     'UnicodeEncodeError': UnicodeEncodeError,
     'UnicodeDecodeError': UnicodeDecodeError,
     'UnicodeTranslateError': UnicodeTranslateError,
     'AssertionError': AssertionError,
     'ArithmeticError': ArithmeticError,
     'FloatingPointError': FloatingPointError,
     'OverflowError': OverflowError,
     'ZeroDivisionError': ZeroDivisionError,
     'SystemError': SystemError,
     'ReferenceError': ReferenceError,
     'MemoryError': MemoryError,
     'BufferError': BufferError,
     'Warning': Warning,
     'UserWarning': UserWarning,
     'DeprecationWarning': DeprecationWarning,
     'PendingDeprecationWarning': PendingDeprecationWarning,
     'SyntaxWarning': SyntaxWarning,
     'RuntimeWarning': RuntimeWarning,
     'FutureWarning': FutureWarning,
     'ImportWarning': ImportWarning,
     'UnicodeWarning': UnicodeWarning,
     'BytesWarning': BytesWarning,
     'ResourceWarning': ResourceWarning,
     'ConnectionError': ConnectionError,
     'BlockingIOError': BlockingIOError,
     'BrokenPipeError': BrokenPipeError,
     'ChildProcessError': ChildProcessError,
     'ConnectionAbortedError': ConnectionAbortedError,
     'ConnectionRefusedError': ConnectionRefusedError,
     'ConnectionResetError': ConnectionResetError,
     'FileExistsError': FileExistsError,
     'FileNotFoundError': FileNotFoundError,
     'IsADirectoryError': IsADirectoryError,
     'NotADirectoryError': NotADirectoryError,
     'InterruptedError': InterruptedError,
     'PermissionError': PermissionError,
     'ProcessLookupError': ProcessLookupError,
     'TimeoutError': TimeoutError,
     'open': <function io.open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)>,
     'copyright': Copyright (c) 2001-2021 Python Software Foundation.
     All Rights Reserved.

     Copyright (c) 2000 BeOpen.com.
     All Rights Reserved.

     Copyright (c) 1995-2001 Corporation for National Research Initiatives.
     All Rights Reserved.

     Copyright (c) 1991-1995 Stichting Mathematisch Centrum, Amsterdam.
     All Rights Reserved.,
     'credits':     Thanks to CWI, CNRI, BeOpen.com, Zope Corporation and a cast of thousands
         for supporting Python development.  See www.python.org for more information.,
     'license': Type license() to see the full license text,
     'help': Type help() for interactive help, or help(object) for help about object.,
     'execfile': <function _pydev_imps._pydev_execfile.execfile(file, glob=None, loc=None)>,
     'runfile': <function _pydev_bundle.pydev_umd.runfile(filename, args=None, wdir=None, namespace=None)>,
     '__IPYTHON__': True,
     'display': <function IPython.core.display_functions.display(*objs, include=None, exclude=None, metadata=None, transient=None, display_id=None, raw=False, clear=False, **kwargs)>,
     'get_ipython': <bound method InteractiveShell.get_ipython of <ipykernel.zmqshell.ZMQInteractiveShell object at 0x7fd680491370>>}

### `global` namespace

`globals()` keyword is a dictionary of the global$($module$)$ namespace. You can see the `__name__` that you might've seen in my program but didn't exactly know where it comes from! When you execute the file, that file acts like the **entry point** so its `__name__` is default set to `__main__`. That's why there're `if __name__ == '__main__:...` codes out there!

```python
globals()
```

    {'__name__': '__main__',
     '__doc__': 'Automatically created module for IPython interactive environment',
     '__package__': None,
     '__loader__': None,
     '__spec__': None,
     '__builtin__': <module 'builtins' (built-in)>,
     '__builtins__': <module 'builtins' (built-in)>,
     '_ih': ['', 'globals()'],
     '_oh': {},
     '_dh': [PosixPath('/Users/jasonlee/Desktop/AI_STUDY/Python')],
     'In': ['', 'globals()'],
     'Out': {},
     'get_ipython': <bound method InteractiveShell.get_ipython of <ipykernel.zmqshell.ZMQInteractiveShell object at 0x7fd680491370>>,
     'exit': <IPython.core.autocall.ZMQExitAutocall at 0x7fd6804a3a30>,
     'quit': <IPython.core.autocall.ZMQExitAutocall at 0x7fd6804a3a30>,
     '_': '',
     '__': '',
     '___': '',
     '_i': '',
     '_ii': '',
     '_iii': '',
     '_i1': 'globals()'}

Did you notice something? The `builtin` namespace is actually included in the `global` namespace!

### Modify globals

```python
globals()['__name__'] = '__modified__'
globals()['__name__']
```

    '__modified__'

As you can see, you can actually modify the global namespace

### `local` namespace

Local namespace is binded to the current namespace that your code is actually in. The local namespace for a **function** is created when the function is called, and removed when it returns or an execption occurs
To retrieve it, use `locals()`.

Side Note: if you execute `locals()` in the global $($or module$)$ namespace, it does the exact same thing as `globals()`

```python
def local_fn():
    x = 1
    print(locals())

local_fn()
```

    {'x': 1}

As you can see, after we declared the variable `x` with the value 1, you can see that the local namespace contains only `x`. Now, let's try to modify it.

```python
def local_fn():
    x = 1
    print("Before attempt to modify: ",locals())
    locals()['x'] = 99999
    print("After attempt to modify: ",locals())

local_fn()
```

    Before attempt to modify:  {'x': 1}
    After attempt to modify:  {'x': 1}

Notice that even though we tried to assign a new value to the variable `x`, the namespace didn't change!

## `Scope`

A scope is a region where a namespace is directly accessible.

### `nonlocal x`

Within a local namespace, you can only `read` the variables found outside the current namespace. If you every try to `write` to that variable, it will just create a new `local variable` in that innermost scope, unaffecting the outer variable. Below, in `inner()`, x is assigned by 999 but for the second print statement, you can see that the `x = 1` remains unchanged.

```python
def local_fn():
    x = 1
    def inner():
        x = 999
        print(x)

    inner()
    print(x)

local_fn()
```

    999
    1

To rebind the outer-scope variables, you can use `nonlocal` keyword followed by the variable name.

```python
def local_fn():
    x = 1
    def inner():
        nonlocal x
        x = 999
        print(x)
    inner()
    print(x)
local_fn()
```

    999
    999

`nonlocal x` rebinds the outer x's scope to the inner scope. That's why if we do `print(x)` outside the inner, we can see that the value indeed changed.

### `global x`

Simiarly, you can rebind the variables residing in the global namespace into the local function by using `global x` keyword.

```python
def local_fn():
    def inner():
        global x
        x = 999
    inner()

local_fn()
print(x)
```

    999

At first glance, it looks very strange that the last print function actually prints `x` even if we have never created such one. The reason for that is in the `inner()`, we binded the variable x from the global namespace.

### `vars()`

`vars()` is a built-in function that returns the `__dict__` attributes for a module, class, object, or any other object with a `__dict__` attributes.

Notice that some objects such as instances and modules have **writable** `__dict__` dictionary containing the object's attributes. However, some objects like `class` has **read only** `__dict__` to prevent modification. For example, classes use a `types.MappingProxyType` to prevent dictionary modifications.

Without any argument, `vars()` acts the same as `locals()`

```python
class Person:
    def __init__(self):
        pass
```

```python
vars(Person)
```

    mappingproxy({'__module__': '__main__',
                  '__init__': <function __main__.Person.__init__(self)>,
                  '__dict__': <attribute '__dict__' of 'Person' objects>,
                  '__weakref__': <attribute '__weakref__' of 'Person' objects>,
                  '__doc__': None})

```python
Person.__dict__
```

    mappingproxy({'__module__': '__main__',
                  '__init__': <function __main__.Person.__init__(self)>,
                  '__dict__': <attribute '__dict__' of 'Person' objects>,
                  '__weakref__': <attribute '__weakref__' of 'Person' objects>,
                  '__doc__': None})

```python
Person.__dict__['__module__'] = "Let me change"
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    Input In [13], in <module>
    ----> 1 Person.__dict__['__module__'] = "Let me change"


    TypeError: 'mappingproxy' object does not support item assignment

As you can see, the `__dict__` of a class is a types.MappingProxyType which you cannot modify

### Namespace and Scope exercise

Below code is referenced from [documentation](https://docs.python.org/3/tutorial/classes.html)

```python
def scope_test():
    def do_local():
        spam = "local spam" # no effect: local

    def do_nonlocal():
        nonlocal spam # rebind the variable from the enclosing function's scope or the nearest scope.
        spam = "nonlocal spam"

    def do_global():
        global spam # We're dealing with the module namespace! That's why the third print() still says "nonlocal spam"
        spam = "global spam"

    spam = "test spam"
    do_local()
    print("After local assignment:", spam) # out: test spam
    do_nonlocal()
    print("After nonlocal assignment:", spam) # out: nonlocal spam
    do_global()
    print("After global assignment:", spam) # out: nonlocal spam

scope_test()
print("In global scope:", spam) # out: global spam

```

    After local assignment: test spam
    After nonlocal assignment: nonlocal spam
    After global assignment: nonlocal spam
    In global scope: global spam

## `vars(object)`

Return the **dict** attribute for a module, class, instance, or any other object with a **dict** attribute.

Objects such as modules and instances have an updateable **dict** attribute; however, other objects may have write restrictions on their **dict** attributes $($for example, classes use a types.MappingProxyType to prevent direct dictionary updates$)$.

Without an argument, `vars()` acts like `locals()`. Note, the locals dictionary is only useful for reads since updates to the locals dictionary are ignored.

A TypeError exception is raised if an object is specified but it doesn’t have a **dict** attribute (for example, if its class defines the **slots** attribute).
