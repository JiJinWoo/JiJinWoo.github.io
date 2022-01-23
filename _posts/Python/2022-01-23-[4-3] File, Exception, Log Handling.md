---
layout: single
title: "File / Exception / Logging"
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

## Exception

```python
class DivisionBySevenError(Exception):
    def __init__(self, msg):
        self.msg = msg

    def __str__(self):
        return self.msg

class DivisionByOneError(Exception):
    def __init__(self, msg):
        self.msg = msg
    def __str__(self):
        return self.msg

try:
    num1 = int(input("첫번째: "))
    num2 = int(input("두번째: "))
    if(num2 == 7):
        raise DivisionBySevenError("7으로 나누지마라!")
    if(num2 == 1):
        raise DivisionByOneError('1으로 나누지마라!')
    print("{} / {} = {}".format(num1,num2, num1/num2))
except ValueError as err:
    print(err)
except ZeroDivisionError as err:
    print(err)
except DivisionBySevenError as err:
    print(err)
except DivisionByOneError as err:
    print(err)
except Exception: # General Error
    print("알수없는오류")
else:
    print("성공!")
```

<pre>
첫번째: 7
두번째: 1
1으로 나누지마라!!
</pre>

## File

- `text` & `binary` file

### `read`

```python
f = open('yesterday.txt', 'r')
content = f.read()
print(type(content))
print(content)
f.close()
```

<pre>
<class 'str'>
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

</pre>

### `readline()`

```python
f = open('yesterday.txt', 'r') # connect address
# content = f.read()
# print(content)

lyrics = ""

while True:
    line = f.readline()
    if not line:
        break
    lyrics += line.strip() + '\n'

print(lyrics)
f.close()
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

</pre>

### `readlines()`

```python
with open('yesterday.txt','r') as f:
    content = f.readlines() # store in list
    print(type(content))
    print(content)
```

<pre>
<class 'list'>
['Yesterday, all my troubles seemed so far away\n', "Now it looks as though they're here to stay\n", 'oh, I believe in yesterday\n', '\n', "Suddenly, I'm not half the man I used to be\n", "There's a shadow hanging over me\n", 'Oh, yesterday came suddenly.\n', '\n', 'Why she had to go?\n', "I don't know, she wouldn't say\n", 'I said something wrong\n', 'Now I long for yesterday.\n', '\n', 'Yesterday love was such an easy game to play\n', 'Now I need a place to hide away\n', 'Oh, I believe in yesterday.\n', '\n', 'Why she had to go?\n', "I don't know, she wouldn't say\n", 'I said something wrong\n', 'Now I long for yesterday.\n', '\n', 'Yesterday love was such an easy game to play\n', 'Now I need a place to hide away\n', 'Oh, I believe in yesterday...\n']
</pre>

### word stats

```python
f = open('yesterday.txt', 'r')
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

['Yesterday,', 'all', 'my', 'troubles', 'seemed', 'so', 'far', 'away\nNow', 'it', 'looks', 'as', 'though', "they're", 'here', 'to', 'stay\noh,', 'I', 'believe', 'in', 'yesterday\n\nSuddenly,', "I'm", 'not', 'half', 'the', 'man', 'I', 'used', 'to', "be\nThere's", 'a', 'shadow', 'hanging', 'over', 'me\nOh,', 'yesterday', 'came', 'suddenly.\n\nWhy', 'she', 'had', 'to', 'go?\nI', "don't", 'know,', 'she', "wouldn't", 'say\nI', 'said', 'something', 'wrong\nNow', 'I', 'long', 'for', 'yesterday.\n\nYesterday', 'love', 'was', 'such', 'an', 'easy', 'game', 'to', 'play\nNow', 'I', 'need', 'a', 'place', 'to', 'hide', 'away\nOh,', 'I', 'believe', 'in', 'yesterday.\n\nWhy', 'she', 'had', 'to', 'go?\nI', "don't", 'know,', 'she', "wouldn't", 'say\nI', 'said', 'something', 'wrong\nNow', 'I', 'long', 'for', 'yesterday.\n\nYesterday', 'love', 'was', 'such', 'an', 'easy', 'game', 'to', 'play\nNow', 'I', 'need', 'a', 'place', 'to', 'hide', 'away\nOh,', 'I', 'believe', 'in', 'yesterday...\n']
['Yesterday, all my troubles seemed so far away', "Now it looks as though they're here to stay", 'oh, I believe in yesterday', '', "Suddenly, I'm not half the man I used to be", "There's a shadow hanging over me", 'Oh, yesterday came suddenly.', '', 'Why she had to go?', "I don't know, she wouldn't say", 'I said something wrong', 'Now I long for yesterday.', '', 'Yesterday love was such an easy game to play', 'Now I need a place to hide away', 'Oh, I believe in yesterday.', '', 'Why she had to go?', "I don't know, she wouldn't say", 'I said something wrong', 'Now I long for yesterday.', '', 'Yesterday love was such an easy game to play', 'Now I need a place to hide away', 'Oh, I believe in yesterday...', '']
</pre>

## Write

```python
f = open('test.txt', 'w', encoding='utf8')
f.write("hello\nmyname is Jason")
f.close()
```

## append

```python
f = open('test.txt', 'a', encoding='utf8')
f.write('\nwow')
f.write("\nhello~")
f.close()
```

### OS module

```python
import os
try:
    os.mkdir('tester')
except FileExistsError as err:
    print("Already Exists")
```

<pre>
Already Exists
</pre>

```python
print(os.path.exists("test.txt"))
print(os.path.exists("tester"))
print(os.path.isfile(os.path.join('tester','test.txt')))
print(os.path.isfile('test.txt'))
print(os.path.isdir('tester'))
```

<pre>
True
True
True
True
True
</pre>

## shutil module

```python
import shutil

source = "test.txt"
destination = os.path.join("tester",'test.txt')
shutil.copy(source,destination)
```

<pre>
'tester/test.txt'
</pre>

## pathlib module

```python
import pathlib # PATH를 object로 다룸
cwd = pathlib.Path.cwd()
print(cwd)
print(cwd.parent)
print(cwd.parent.parent)
```

<pre>
/Users/jasonlee/Desktop/NAVER Boostcamp AI TECH/Week1/Python
/Users/jasonlee/Desktop/NAVER Boostcamp AI TECH/Week1
/Users/jasonlee/Desktop/NAVER Boostcamp AI TECH
</pre>

## pickle

```python
import pickle

f = open('example.pickle', 'wb')
ex = [1,2,3,4,5]
pickle.dump(ex, f)
f.close()
```

```python
f = open('example.pickle','rb')
content = pickle.load(f)
print(content)
f.close()
```

<pre>
[1, 2, 3, 4, 5]
</pre>

## Logging

- debug > info > warning > error > critical

```python
import logging
logger = logging.getLogger('main')
logging.basicConfig(level=logging.DEBUG)
# logger.setLevel(logging.DEBUG)

steam_handler = logging.FileHandler(
    "my.log", mode='a', encoding='utf8'
)

logger.addHandler(steam_handler)

logger.debug('wrong')
logger.info('check')
logger.warning('warning')
logger.error('error')
logger.critical("disaster")
```

<pre>
DEBUG:main:wrong
INFO:main:check
WARNING:main:warning
ERROR:main:error
CRITICAL:main:disaster
</pre>

### argparse

```python

```
