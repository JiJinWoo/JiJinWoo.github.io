---
layout: single
title: "[Python] Conditionals and Loops"
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

## Compare Operators

<code>x == y</code>: value

<code>x is y</code>: value and memory

```python
a = [1, 2, 3, 4, 5]
b = [1, 2, 3, 4, 5]
print(a == b)
print(a is b)
```

<pre>
True
False
</pre>

**[Important]** There's reserved memory space -5 ~ 256 (shared memory)

```python
a = 256
b = 256
print(a == b)
print(a is b)
```

<pre>
True
True
</pre>

```python
a = 257
b = 257
print(a == b)
print(a is b)
```

<pre>
True
False
</pre>

## True and False

- <code>int</code>: <code>1</code> **True**, else False

- <code>str</code>: <code>""</code> **False**, else True

<code>all()</code> <code>any()</code>

```python
b = [True, False, True]
print(all(b)) # AND - True if everything is true
print(any(b)) # OR - True of any is true
```

<pre>
False
True
</pre>

## for

<code>for i in range(x,y,z)</code>: increment by <code>z</code> from <code>x</code> to <code>y-1</code>

```python
for i in range(2, 10, 2): # [2,10) +2
    print(i, end="")
print("\n")
for i in range(11, 1, -2): # [11, 1) -2
    print(i, end="")
```

<pre>
2468

119753
</pre>

```python

```
