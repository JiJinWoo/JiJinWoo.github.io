---
layout: single
title:  "Data Structures"
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

  .page__content p {
      margin: 0 0 0px !important;
  }

  .page__content p > strong {
    font-size: 0.8rem !important;
  }

  </style>
</head>


### Stack



```python
stk = []
stk.append(0)
stk.append(1)
stk.append(2)
print(stk)
stk.pop()
print(stk)
```

<pre>
[0, 1, 2]
[0, 1]
</pre>
## Queue



```python
q = []
q.append(1)
q.append(2)
q.append(3)
print(q)
q.pop(0)
print(q)
```

<pre>
[1, 2, 3]
[2, 3]
</pre>
## Set



```python
s = set([1,2,3])
s2 = {4,5,6,6}
```


```python
s.add(4)
print(s)
```

<pre>
{1, 2, 3, 4}
</pre>

```python
s.remove(4)
print(s)
```

<pre>
{1, 2, 3}
</pre>

```python
s.update([5])
print(s)
```

<pre>
{1, 2, 3, 5}
</pre>

```python
s.discard(5)
print(s)
```

<pre>
{1, 2, 3}
</pre>

```python
s1 = set([1,2,3])
s2 = set([2,3,4])
print(s1.union(s2))
print(s1 | s2)
print(s1.intersection(s2))
print(s1 & s2)
print(s1.difference(s2))
print(s1 - s2)
```

<pre>
{1, 2, 3, 4}
{1, 2, 3, 4}
{2, 3}
{2, 3}
{1}
{1}
</pre>
## Dict



```python
d = {'jason':82, 'marry':17, 'jon':32}
```


```python
print(d.items())
for e in d.items():
    print(e, end=" ")
```

<pre>
dict_items([('jason', 82), ('marry', 17), ('jon', 32)])
('jason', 82) ('marry', 17) ('jon', 32) 
</pre>

```python
for key in d.keys():
    print(d[key], end=" ")
```

<pre>
82 17 32 
</pre>

```python
d.pop('jason')
print(d)
```

<pre>
{'marry': 17, 'jon': 32}
</pre>

```python
d['jason'] = 82
print(d)

d.popitem()
print(d)
```

<pre>
{'marry': 17, 'jon': 32, 'jason': 82}
{'marry': 17, 'jon': 32}
</pre>

```python
d.popitem()
print(d)
```

<pre>
{'marry': 17}
</pre>
## collections module



```python
from collections import deque
from collections import Counter
from collections import OrderedDict
from collections import defaultdict
from collections import namedtuple
```

## deque



```python
deq = deque()
deq.append(1)
deq.append(2)
print(deq)
deq.appendleft(3)
print(deq)
deq.pop()
print(deq)
deq.popleft()
print(deq)
```

<pre>
deque([1, 2])
deque([3, 1, 2])
deque([3, 1])
deque([1])
</pre>

```python
deq.append(3)
deq.appendleft(2)
print(deq)
```

<pre>
deque([2, 1, 3])
</pre>

```python
deq.rotate(2)
print(deq)
```

<pre>
deque([2, 1, 3])
</pre>

```python
print(deq)
deq.extend([1])
deq.extend([1,2,3])
print(deq)
```

<pre>
deque([2, 1, 3])
deque([2, 1, 3, 1, 1, 2, 3])
</pre>
## OrderedDict (obselete)



```python
d = OrderedDict({'jason':82, 'zarry':17, 'aon':32})
d2 = {'jason':82, 'zarry':17, 'aon':32}

for k,v in d.items():
    print(k,v)

print('*'*10)
for k,v in d2.items():
    print(k,v)
```

<pre>
jason 82
zarry 17
aon 32
**********
jason 82
zarry 17
aon 32
</pre>
## defaultdict



frequency 사용할때도 유용함



```python
d = defaultdict(lambda: 0) # default (기본값) 설정
```


```python
d['first'] # 아무것도 없는데 설정됨
```

<pre>
0
</pre>
## Counter

-> set 연산도 가능



```python
c = Counter()
c
```

<pre>
Counter()
</pre>

```python
c = Counter('sadfasdwlefw') # dictionary 반환
c
```

<pre>
Counter({'s': 2, 'a': 2, 'd': 2, 'f': 2, 'w': 2, 'l': 1, 'e': 1})
</pre>

```python
c = Counter({'a' : 2, 'b' : 3, 'c' : 6})
list(c.elements())
```

<pre>
['a', 'a', 'b', 'b', 'b', 'c', 'c', 'c', 'c', 'c', 'c']
</pre>
## namedtuple



```python
Point = namedtuple('Point', ['x','y'])
p = Point(x=11, y=22)
print(p[0], p[1])
print(p.x, p.y)
```

<pre>
11 22
11 22
</pre>

```python
p.x, p.y
```
