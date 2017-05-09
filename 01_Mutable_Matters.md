## Creating a length-N empty list or list with the same thing
List is mutabl!!

```
>>> _lists = [[]] * 4
>>> _lists[0].append("mutable")
>>> print(_lists)
[['mutable'], ['mutable'], ['mutable'], ['mutable']]
```

```
>>> _lists = [[] for __ in range(4)]
>>> _lists[0].append("mutable")
>>> print(_lists)
[['mutable'], [], [], []]
```

## Mutable Default Arguments (from http://python-guide-pt-br.readthedocs.io/en/latest/writing/gotchas/)
Python’s default arguments are evaluated once when the function is defined!!

```
def append_to(element, to=[]):
    to.append(element)
    return to
    
my_list = append_to(12)
print my_list

my_other_list = append_to(42)
print my_other_list
```

Results
```
[12]
[12, 42]
```

```
def append_to(element, to=None):
    if to is None:
        to = []
    to.append(element)
    return to
```

## Deep Copy list (from https://www.reddit.com/r/learnpython/comments/1afldr/why_is_copying_a_list_so_damn_difficult_in_python/)
```
foo = [[1,2], [3,4], [5,6]]
bar = foo # doesnt work
bar = foo[:] # doesnt work
bar = list(foo) # doesnt work
bar = list(foo[:]) # doesnt work
bar = []
bar += foo # doesnt work
bar = []
bar.append(foo) # doesnt work
for i, x in enumerate(foo):
    bar[i] = x[:]
# didnt work
```

```
bar = [x[:] for x in foo]

import copy
bar = copy.deepcopy(foo)
```
