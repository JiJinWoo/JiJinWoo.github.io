---
layout: single
title:  "Pythonic Code"
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


* `split`, `join`

* list comprehension

* `enumerate`, `zip`

* `lambda`, `map`, `reduce`

* `generator`

* `asterisk`


### `split`



```python
items = "jason.marry.jonathan.joseph".split('.')
items
```

<pre>
['jason', 'marry', 'jonathan', 'joseph']
</pre>
### `join`



```python
colors = ['red','blue','green']
result = '-'.join(colors)
result
```

<pre>
'red-blue-green'
</pre>
## list comprehension

* 기존 list를 사용해서 간단히 다른 list를 만드는 기법



```python
s = [i for i in range(10)]
s
```

<pre>
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
</pre>

```python
s = [i for i in range(10) if i%2==0]
s
```

<pre>
[0, 2, 4, 6, 8]
</pre>

```python
w1 = "Hello"
w2 = "World"
res = [i+j for i in w1 for j in w2 if i!=j] # nested for loop -> only if
print(res, end=" ")
```

<pre>
['HW', 'Ho', 'Hr', 'Hl', 'Hd', 'eW', 'eo', 'er', 'el', 'ed', 'lW', 'lo', 'lr', 'ld', 'lW', 'lo', 'lr', 'ld', 'oW', 'or', 'ol', 'od'] 
</pre>

```python
w1 = "Hello"
w2 = "World"
res = [i+j if i!=j else i for i in w1 for j in w2] # nested for loop -> both if/else -> 뒤에 loop가 먼저 작동
print(res, end=" ")
```

<pre>
['HW', 'Ho', 'Hr', 'Hl', 'Hd', 'eW', 'eo', 'er', 'el', 'ed', 'lW', 'lo', 'lr', 'l', 'ld', 'lW', 'lo', 'lr', 'l', 'ld', 'oW', 'o', 'or', 'ol', 'od'] 
</pre>

```python
import pprint

sentence = 'hello my name is jason'.split()
pprint.pprint([[w.upper(), w.lower(), len(w)] for w in sentence])
```

<pre>
[['HELLO', 'hello', 5],
 ['MY', 'my', 2],
 ['NAME', 'name', 4],
 ['IS', 'is', 2],
 ['JASON', 'jason', 5]]
</pre>
### `enumerate`



```python
s = 'ABCD'
{v : i for i,v in enumerate(s)}
```

<pre>
{'A': 0, 'B': 1, 'C': 2, 'D': 3}
</pre>
### `zip`

* 두개의 list의 값을 병렬적으로 추출



```python
a = ['a1','a2','a3']
b = ['b1','b2','b3']
[[a,b] for a,b in zip(a,b)]
[(a,b) for a,b in zip(a,b)]
[z for z in zip(a,b)]
```

<pre>
[('a1', 'b1'), ('a2', 'b2'), ('a3', 'b3')]
</pre>
### `enumerate` & `zip`



```python
a = ['a1','a2','a3']
b = ['b1','b2','b3']

list(enumerate(zip(a,b)))
```

<pre>
[(0, ('a1', 'b1')), (1, ('a2', 'b2')), (2, ('a3', 'b3'))]
</pre>
### `lambda` - 권장 X



```python
(lambda x,y : x + y)(10,20)
```

<pre>
30
</pre>
### `map`



```python
ex = [1,2,3,4,5]
f = lambda x: x ** 2

list(map(f, ex))
```

<pre>
[1, 4, 9, 16, 25]
</pre>

```python
f = lambda x, y : x + y
list(map(f, ex, ex))
```

<pre>
[2, 4, 6, 8, 10]
</pre>

```python
list(map(lambda x: x ** 2 if x % 2 == 0 else 0, ex))
```

<pre>
[0, 4, 0, 16, 0]
</pre>
### `reduce`



```python
from functools import reduce
reduce(lambda x, y: x+y, [1,2,3,4,5])
```

<pre>
15
</pre>
## iterable object



```python
a = ['jaosn','memory','freesia']

memory_address = iter(a) # a[0]의 메모리 주소 반환
print(next(memory_address))
print(next(memory_address))
print(next(memory_address))
```

<pre>
jaosn
memory
freesia
</pre>
## generator

* iterable object를 특수한 형태로 사용해주는 함수

* element가 사용되는시점에 값을 메모리에 반환

    * yield를 사용해 한번에 하나의 element만 반환함

* list타입의 데이터를 반환해주는 함수는 generator로 만들자!

* 큰 데이터 처리할때 -> generator expression

* 파일 데이터도 generator



```python
def general_list(value):
    result = []
    for i in range(value):
        result.append(i)
    return result
```


```python
print(general_list(50))
```

<pre>
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49]
</pre>

```python
import sys
result = general_list(50)
sys.getsizeof(result)
```

<pre>
472
</pre>

```python
def generator_list(value):
    result = []
    for i in range(value):
        yield i
```


```python
for a in generator_list(50):
    print(a, end=" ")
```

<pre>
0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 
</pre>

```python
result = generator_list(50)
sys.getsizeof(result)
```

<pre>
112
</pre>

```python
gen_ex = (n*n for n in range(500))
print(type(gen_ex))
```

<pre>
<class 'generator'>
</pre>

```python
print(list(gen_ex))
```

<pre>
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81, 100, 121, 144, 169, 196, 225, 256, 289, 324, 361, 400, 441, 484, 529, 576, 625, 676, 729, 784, 841, 900, 961, 1024, 1089, 1156, 1225, 1296, 1369, 1444, 1521, 1600, 1681, 1764, 1849, 1936, 2025, 2116, 2209, 2304, 2401, 2500, 2601, 2704, 2809, 2916, 3025, 3136, 3249, 3364, 3481, 3600, 3721, 3844, 3969, 4096, 4225, 4356, 4489, 4624, 4761, 4900, 5041, 5184, 5329, 5476, 5625, 5776, 5929, 6084, 6241, 6400, 6561, 6724, 6889, 7056, 7225, 7396, 7569, 7744, 7921, 8100, 8281, 8464, 8649, 8836, 9025, 9216, 9409, 9604, 9801, 10000, 10201, 10404, 10609, 10816, 11025, 11236, 11449, 11664, 11881, 12100, 12321, 12544, 12769, 12996, 13225, 13456, 13689, 13924, 14161, 14400, 14641, 14884, 15129, 15376, 15625, 15876, 16129, 16384, 16641, 16900, 17161, 17424, 17689, 17956, 18225, 18496, 18769, 19044, 19321, 19600, 19881, 20164, 20449, 20736, 21025, 21316, 21609, 21904, 22201, 22500, 22801, 23104, 23409, 23716, 24025, 24336, 24649, 24964, 25281, 25600, 25921, 26244, 26569, 26896, 27225, 27556, 27889, 28224, 28561, 28900, 29241, 29584, 29929, 30276, 30625, 30976, 31329, 31684, 32041, 32400, 32761, 33124, 33489, 33856, 34225, 34596, 34969, 35344, 35721, 36100, 36481, 36864, 37249, 37636, 38025, 38416, 38809, 39204, 39601, 40000, 40401, 40804, 41209, 41616, 42025, 42436, 42849, 43264, 43681, 44100, 44521, 44944, 45369, 45796, 46225, 46656, 47089, 47524, 47961, 48400, 48841, 49284, 49729, 50176, 50625, 51076, 51529, 51984, 52441, 52900, 53361, 53824, 54289, 54756, 55225, 55696, 56169, 56644, 57121, 57600, 58081, 58564, 59049, 59536, 60025, 60516, 61009, 61504, 62001, 62500, 63001, 63504, 64009, 64516, 65025, 65536, 66049, 66564, 67081, 67600, 68121, 68644, 69169, 69696, 70225, 70756, 71289, 71824, 72361, 72900, 73441, 73984, 74529, 75076, 75625, 76176, 76729, 77284, 77841, 78400, 78961, 79524, 80089, 80656, 81225, 81796, 82369, 82944, 83521, 84100, 84681, 85264, 85849, 86436, 87025, 87616, 88209, 88804, 89401, 90000, 90601, 91204, 91809, 92416, 93025, 93636, 94249, 94864, 95481, 96100, 96721, 97344, 97969, 98596, 99225, 99856, 100489, 101124, 101761, 102400, 103041, 103684, 104329, 104976, 105625, 106276, 106929, 107584, 108241, 108900, 109561, 110224, 110889, 111556, 112225, 112896, 113569, 114244, 114921, 115600, 116281, 116964, 117649, 118336, 119025, 119716, 120409, 121104, 121801, 122500, 123201, 123904, 124609, 125316, 126025, 126736, 127449, 128164, 128881, 129600, 130321, 131044, 131769, 132496, 133225, 133956, 134689, 135424, 136161, 136900, 137641, 138384, 139129, 139876, 140625, 141376, 142129, 142884, 143641, 144400, 145161, 145924, 146689, 147456, 148225, 148996, 149769, 150544, 151321, 152100, 152881, 153664, 154449, 155236, 156025, 156816, 157609, 158404, 159201, 160000, 160801, 161604, 162409, 163216, 164025, 164836, 165649, 166464, 167281, 168100, 168921, 169744, 170569, 171396, 172225, 173056, 173889, 174724, 175561, 176400, 177241, 178084, 178929, 179776, 180625, 181476, 182329, 183184, 184041, 184900, 185761, 186624, 187489, 188356, 189225, 190096, 190969, 191844, 192721, 193600, 194481, 195364, 196249, 197136, 198025, 198916, 199809, 200704, 201601, 202500, 203401, 204304, 205209, 206116, 207025, 207936, 208849, 209764, 210681, 211600, 212521, 213444, 214369, 215296, 216225, 217156, 218089, 219024, 219961, 220900, 221841, 222784, 223729, 224676, 225625, 226576, 227529, 228484, 229441, 230400, 231361, 232324, 233289, 234256, 235225, 236196, 237169, 238144, 239121, 240100, 241081, 242064, 243049, 244036, 245025, 246016, 247009, 248004, 249001]
</pre>
## arguments


* Keyword argument

* Default argument

* variable-length argument


### variable-length argument

* asterisk must be the last argument

* tuple type



```python
def help(a, b, *args): # tuple
    return a + b + sum(args)

help(1,2,5,3,3,1,3,3,3)
```

<pre>
24
</pre>
### keyword variable length

* dict type



```python
def help(**kwargs):
    print(kwargs)
    
help(a=1, b=3, c=5)
```

<pre>
{'a': 1, 'b': 3, 'c': 5}
</pre>
## asterisk - unpacking a container



```python
def help(a, *args):
    print(a, *args) # unpacking
    print(a, args)
    print(type(args))
    
help(1, *(2,3,4,5,6)) # unpacking
```

<pre>
1 2 3 4 5 6
1 (2, 3, 4, 5, 6)
<class 'tuple'>
</pre>

```python
x = [6,7,8,6]
print(x)
print(*x)
```

<pre>
[6, 7, 8, 6]
6 7 8 6
</pre>

```python
x = ([1,2],[3,4],[5,6])
print(*x)
```

<pre>
[1, 2] [3, 4] [5, 6]
</pre>

```python
def test(**kwargs):
    print(kwargs)
    
x = {'a':1, 'b':2, 'c':3}
test(**x)
```

<pre>
{'a': 1, 'b': 2, 'c': 3}
</pre>

```python
x = ([1,2],[3,4],[5,6])
for v in zip(*x):
    print(v)
```

<pre>
(1, 3, 5)
(2, 4, 6)
</pre>

```python
```
