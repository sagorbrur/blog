---
title: Working with directory in python
---

Working with multiple directory is one of the trickiest work in python.
We will solve this trickiest work in simple way.

## Defining base path using `os.getcwd()`

we will define currect working directory as basepath. 

Our working path is 'home/sagor/Desktop/hello'

```py
import os

BASE_PATH = os.getcwd()
print(BASE_PATH)
# output: home/sagor/Desktop/hello

```

Done! initializing base path

Now we have three folder inside hello. 

* src (contains source script)
* data (contains data files)
* logs (contains our logs file)

## Adding these path to our base path using `os.path.join`

Now we add these path to our base path. 

```py
SRC_PATH = os.path.join(BASE_PATH, 'src')
DATA_PATH = os.path.join(BASE_PATH, 'data')
LOGS_PATH = os.path.join(BASE_PATH, 'logs')


# if we have a folder 'extra' outside 'hello', we can add too.

EXTRA_PATH = os.path.join(BASE_PATH, '../hello')


```


Now you can work these defined path inside your basepath.

## Exampe work

We will print all the files inside `DATA_PATH` using `os.listdir`

```py

files = os.listdir(DATA_PATH)

for file in files:
    print(file)
    
# output: 'hello.png''hello1.png'


```
