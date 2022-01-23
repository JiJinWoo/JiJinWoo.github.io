---
layout: single
title: "Function and Console I/O"
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

## formatting output

- <code>%</code>, <code>format</code>, <code>fstring</code>

## <code>%</code>

```python
print('%s %s' % ('hello', 'jason'))
print('%d %s %f' % (10, 'jason', 10.2))
```

<pre>
hello jason
10 jason 10.200000
</pre>

```python
print("%10s" % ("Jason"))
print("%10.5f" % (1/7))
```

<pre>
     Jason
   0.14286
</pre>

```python
print("Name: %(name)10s" % {"name":"jason"})
```

<pre>
Name:      jason
</pre>

## <code>.format()</code>

```python
print('hello {} my name if {}'.format("jason","chilla"))
print('hello {0} my name if {1}'.format("jason","chilla"))
print('hello {0:10.5f} my name if {1}'.format(1/7,"chilla"))
print('hello {you} my name if {me}'.format(you="jason", me="chilla"))
```

<pre>
hello jason my name if chilla
hello jason my name if chilla
hello    0.14286 my name if chilla
hello jason my name if chilla
</pre>

#### padding

```python
print("Name: {:>20.5}".format("Jason"))
```

<pre>
Name:                Jason
</pre>

## <code>fstring</code>

```python
name = "Jason"
age = 26
school = "skrt"
amount = 254.2
print(f"{name:*>20}")
print(f"{name:*<20}")
print(f"{name:*^20}")
print(f"{amount:.2f}")
```

<pre>
***************Jason
Jason***************
*******Jason********
254.20
</pre>

```python

```
