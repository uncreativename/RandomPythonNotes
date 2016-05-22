# Python Notes

### Header

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
```
----

### Useful functions for figuring out how things work
* help()
* dir()
* type()

-----------

Print docstring of class or function

```python
print(function_or_class.__doc__)
```

--------------
### List Comprehensions

```python
# matrix
mylist = [[1, 2, 3],
          [4, 5, 6],
          [7, 8, 9]]
```

```python
col2 = [row[1] for row in mylist]
```

=> [2, 5, 8]

------

Does the same as above but demonstrates why comprehensions are awesome
```python
col2 = []
for row in mylist:
    col2.append(row[1])
```

-------

Expressions also work in comprehensions

```python
col3 = [row[1] + 1 for row in mylist]
```
=> [3, 6, 9]

-------

Returns 2nd column without odd numbers
```python
col2 = [row[1] for row in mylist if row[1] % 2 == 0]
```
=> [2, 8]

----------

Gets diagonal

```python
diag = [mylist[i][i] for i in [0, 1, 2]]
```
=> [1, 5, 9]

--------

Another way to get diagonal
```python
diag2 = [mylist[i][i] for i in range(3)]
```
=> [1, 5, 9]

-----

`mylist`

|||||
|---|---|---|---|
| 1 | 2 | 3 | -->  6 |
| 4 | 5 | 6 | -->  15 |
| 7 | 8 | 9 | -->  24 |

-----

Create a set of summed rows from list comprehension (no order)

```python
{sum(row) for row in mylist}
```

=> {24, 6, 15}

-------

Create dictionary from list comprehension

```python
{i: sum(mylist[i]) for i in range(3)}
```

=> {0: 6, 1: 15, 2: 24}

-----------

Create generator from list comprehension (2nd column of `mylist`)

```python
gen_col2 = (row[1] for row in mylist)
```

=> [2, 5, 8]

-------------------

Different ways to access gen_col2 items

```python
gen_col2.__next__()
```
=> 2

```python
next(gen_col2)
```
=> 5

```python
gen_col2.__next__()
```
=> 8

------

Access gen_col2 with a loop

You can only consume the values of a generator once so we must call this again:  
`gen_col2 = (row[1] for row in mylist)`

```python
for x in gen_col2:
    print(x)
```

=> 2, 5, 8

--------

**Reminder**

`mylist`

|||||
|---|---|---|---|
| 1 | 2 | 3 | -->  6 |
| 4 | 5 | 6 | -->  15 |
| 7 | 8 | 9 | -->  24 |

-------------------

Returns sum of each row and returns result as a list;

```python
sums = list(map(sum, mylist))
```

=> [6, 15, 24]

------------------

Repeat characters

```python
doubles = [char * 2 for char in 'spam']
```

=> ['ss', 'pp', 'aa', 'mm']

---------------------

Can use more than 1 list in list comprehension

```python
S = [x for x in range(1000000)]
T = [y**2 for y in range(300)]

[x for x in T if x in S]
```
------------------------------

### Using range

```python
list(range(4))
```

=> [0, 1, 2, 3]

--------

range(start, stop, step)

```python
list(range(-6, 7, 2))
```

=> [-6, -4, -2, 0, 2, 4, 6]

-----

```python
[[x ** 2, x ** 3] for x in range(4)]
```

=> [ [0, 0], [1, 1], [4, 8], [9, 27] ]

----------

```python
[[x, x / 2, x * 2] for x in range(-6, 7, 2) if x > 0]
```

=> [ [2, 1.0, 4], [4, 2.0, 8], [6, 3.0, 12] ]

-----------

Same as above

```python
m_list = []
for x in range(-6, 7, 2):
    if x > 0:
        m_list.append([x, x / 2, x * 2])
```

=> [ [2, 1.0, 4], [4, 2.0, 8], [6, 3.0, 12] ]

---------------

### Closures: Using values out of scope

Closures can avoid the use of global values and provides some form of data hiding. It can also provide an object oriented solution to the problem. When there are few methods (one method in most cases) to be implemented in a class, closures can provide an alternate and more elegant solutions. But when the number of attributes and methods get larger, better implement a class.

```python
def make_multiplier_of(n):
    def multiplier(x):
        return x * n
    return multiplier
```

```python
times3 = make_multiplier_of(3)
times5 = make_multiplier_of(5)
```
-----

```python
times3(9)
```
=> 27

```python
times5(3)
```
=> 15

```python
times5(times3(2))
```
=> 30

--------------

### Get file as string

```python
with open ("data.txt", "r") as myfile:
    data = myfile.read()
```

----------------

### Ipdb Debugging

```python
import ipdb
ipdb.set_trace()
```

`p` print  
`pp` pretty print  
`n` next  
`s` step  
`c` continue  
`l` list out code(optional arguments for lines[l #, #] or [l #])  
`a` args (prints out all the arguments the current function received)  
`j` jump to given line  

pp locals()
pp globals()

https://pythonadventures.wordpress.com/tag/ipdb/

---------------

Use these commands to see all variables in the given scope, local or global. This is super useful for a quick glance at all the objects your program has access to at that moment.

```python
pp locals()
pp globals()
```

--------

### Resources

[quick basics] http://learnxinyminutes.com/docs/python/  
http://www.diveintopython3.net/  
http://docs.python-guide.org/en/latest/  
[cool libraries] https://github.com/vinta/awesome-python  
http://www.python-course.eu/python3_course.php  
http://www.programiz.com/python-programming  
http://treyhunner.com/2015/12/python-list-comprehensions-now-in-color/


### Books
Fluent Python
python cookbook
learning python  
programming python

-------

### timeit

```python
def my_function():
    l = [i for i in range(50)]

if __name__ == "__main__":
    import timeit
    setup = "from __main__ import my_function"
    print(timeit.timeit("my_function()", setup=setup))
```
=> 2.533552071000031

--------------------

### Hackerank IO

```python
#!/bin/python3

import sys

n = int(input().strip())
arr = [int(arr_temp) for arr_temp in input().strip().split(' ')]
```

split between 2 variables

```python
import sys

T = int(input().strip())
for a0 in range(T):
    n,k = input().strip().split(' ')
    n,k = [int(n),int(k)]
```

------------

### Count positive, negative, and zeros in list

```python
pos = sum(i > 0 for i in arr)
neg = sum(i < 0 for i in arr)
zero = sum(i == 0 for i in arr)
```
---------------------------------

### Things to add
doing list and set operations with comprehensions  
zip  
lambda, map, filter, reduce  
*args, **kwargs  
getattr/setattr  
generators  
any, all functions  
partial()  
iter()  

itertools:  
chain  
combinations/permutations  
compress  
count  
cycle  
groupby  
product  

-----------------------

http://stackoverflow.com/questions/19389490/how-pythons-any-and-all-functions-work

Brett Slatkin - How to Be More Effective with Functions - PyCon 2015
https://www.youtube.com/watch?v=WjJUPxKB164

Raymond Hettinger: Transforming Code into Beautiful, Idiomatic Python
https://www.youtube.com/watch?v=OSGv2VnC0go

Raymond Chandler - Super Advanced Python
https://www.youtube.com/watch?v=u2KZJzoz-qI
