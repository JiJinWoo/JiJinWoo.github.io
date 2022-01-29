---
layout: single
title: "Strings / Advanced Functions"
categories: Python
tag: [python]
author_profile: true
sidebar_main: true
---

<head>
  <style>
    table.dataframe {
      white-space: normal;
      width: 100%;
      height: 240px;
      display: block;
      overflow: auto;
      font-family: Arial, sans-serif;
      font-size: 0.9rem;
      line-height: 20px;
      text-align: center;
      border: 0px !important;
    }

    table.dataframe th {
      text-align: center;
      font-weight: bold;
      padding: 8px;
    }

    table.dataframe td {
      text-align: center;
      padding: 8px;
    }

    table.dataframe tr:hover {
      background: #b8d1f3;
    }

    .output_prompt {
      overflow: auto;
      font-size: 0.9rem;
      line-height: 1.45;
      border-radius: 0.3rem;
      -webkit-overflow-scrolling: touch;
      padding: 0.8rem;
      margin-top: 0;
      margin-bottom: 15px;
      font: 1rem Consolas, "Liberation Mono", Menlo, Courier, monospace;
      color: $code-text-color;
      border: solid 1px $border-color;
      border-radius: 0.3rem;
      word-break: normal;
      white-space: pre;
    }

.dataframe tbody tr th:only-of-type {
vertical-align: middle;
}

.dataframe tbody tr th {
vertical-align: top;
}

.dataframe thead th {
text-align: center !important;
padding: 8px;
}

.page\_\_content p {
margin: 0 0 0px !important;
}

.page\_\_content p > strong {
font-size: 0.8rem !important;
}

  </style>
</head>

## String

- store <code>char</code> data in sequence

- `char`: 1byte

- `1byte` = `8bit` = 256

- converts `bit` to `char` or vice-versa according to rules (UTF-8, ASCII, etc)

* `int` = `4byte` = $-2^{31}\sim2^{31} - 1$

#### Slicing `a[::]`

```python
a = [1,2,3,4,5]
s = "hello jason"

print(a[::-1])
print(a[::3])
print(s[::-1])
```

<pre>
[5, 4, 3, 2, 1]
[1, 4]
nosaj olleh
</pre>

#### `a.upper()` `a.lower()`

```python
a = 'xYzDfSFs'
print(a.upper())
print(a.lower())
```

<pre>
XYZDFSFS
xyzdfsfs
</pre>

#### `a.capitalize()`: capitalize first char

```python
a = 'xYzDfSFs'
a.capitalize()
```

<pre>
'Xyzdfsfs'
</pre>

#### `a.count('xyz')`: # of 'abc' in a

```python
a = 'xyzdfsfasfxyzxyz'
a.count('xyz')
```

<pre>
3
</pre>

#### `a.find('xyz')`: return offset of 'xyz'

```python
a = 'aaaxyzdfsfasfxyzxyz'
a.find('xyz')
```

<pre>
3
</pre>

#### `a.startswith('xyz')` `a.endswith('xyz')`: whether a starts/ends with 'xyz'

```python
a = 'xyzdfsfasfxyzxyz'
print(a.startswith('xyz'))
print(a.endswith('xyz'))
```

<pre>
True
True
</pre>

#### `r""`: raw string

```python
sentence = 'hello it\'s me'
raw_sentence = r'hello it\'s me'
print(i)
print(raw_sentence)
```

<pre>
hello it's me
hello it\'s me
</pre>

#### `a.strip()`: remove space front/back

```python
a = "    hello    "
a.strip()
```

<pre>
'hello'
</pre>

#### `copy.deepcopy()`

```python
import copy
a = [[1,2,3],[4,5,6]]
b = copy.deepcopy(a)
b[0][0] = 100
print(a)
print(b)
```

<pre>
[[1, 2, 3], [4, 5, 6]]
[[100, 2, 3], [4, 5, 6]]
</pre>

### Lab 1

```python
!wget https://raw.githubusercontent.com/TeamLab/introduction_to_python_TEAMLAB_MOOC/master/code/6/yesterday.txt
```

<pre>
--2022-01-18 13:08:43--  https://raw.githubusercontent.com/TeamLab/introduction_to_python_TEAMLAB_MOOC/master/code/6/yesterday.txt
Resolving raw.githubusercontent.com... 185.199.108.133, 185.199.109.133, 185.199.111.133, ...
Connecting to raw.githubusercontent.com|185.199.108.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 638 [text/plain]
Saving to: 'yesterday.txt'

yesterday.txt       100%[===================>]     638  --.-KB/s    in 0s      

2022-01-18 13:08:44 (24.3 MB/s) - 'yesterday.txt' saved [638/638]

</pre>

```python
lyrics = ""

with open('yesterday.txt', 'r') as f:
    while True:
        line = f.readline()
        if not line:
            break
        lyrics += line.strip() + "\n"

print(lyrics)

print(lyrics.count('yesterday'))
print(lyrics.count('YESTERDAY'))
```

<pre>
Yesterday, all my troubles seemed so far away
Now it looks as though they're here to stay
oh, I believe in yesterday

Suddenly, I'm not half the man I used to be
There's a shadow hanging over me
Oh, yesterday came suddenly.

Why she had to go?
I don't know, she wouldn't say
I said something wrong
Now I long for yesterday.

Yesterday love was such an easy game to play
Now I need a place to hide away
Oh, I believe in yesterday.

Why she had to go?
I don't know, she wouldn't say
I said something wrong
Now I long for yesterday.

Yesterday love was such an easy game to play
Now I need a place to hide away
Oh, I believe in yesterday...

6
0
</pre>

## Advanced Function Concepts

#### Call by `Value`

```python
def change(x):
    x += 1
    return x

x = 10
change(x)
print(x) # unchanged
```

<pre>
10
</pre>

#### Call by `Object Reference`

- `Address of object` is passed

```python
def modify(arr): # address of object s is passed as parameter
    arr.append(1)
    arr = [1,2,3]

s = [0]
modify(s)
print(s)
```

<pre>
[0, 1]
</pre>

## Scoping

#### Use `global` keyword to use global variable in function

```python
def tester():
    global x # declare that we're using global variable x
    x = 10 # access global variable
    print(x)

x = 20
tester()
print(x) # changed!
```

<pre>
10
10
</pre>

## Function type hints

```python
def test(x: int) -> str:
    return str(x + 10)

print(test(10))
print(type(test(10)))
```

<pre>
20
<class 'str'>
</pre>

## docstring

-> try out docstring extension in vscode!

```python
def add(a: int, b: int) -> int:
    '''
    return
        - the sum of two floats
    parameters
        - a: int
        - b: int
    '''

    return a + b

print(add(3,10))
```

<pre>
13
</pre>

```python

```
