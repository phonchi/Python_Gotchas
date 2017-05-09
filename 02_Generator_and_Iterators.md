## What is differnece between range and xrange?
```
def range(start, stop, step=1):
    numbers = []
    while start < stop:
        numbers.append(start)
        start += step
    return numbers

def xrange(start, stop, step=1):
    while start < stop:
        yield start # 
        start += step
        
```
The first thing to note is that the range implementation must precreate the list of all numbers within the range. 
So, if the range is from 1 to 10,000, the function will do 10,000 appends to the numbers list and then return it. 

On the other hand, the generator is able to "return" many values. Every time the code gets to the yield, the function 
emits its value, and when another value is requested the function resumes running (maintaining its previous
state) and emits the new value. When the function reaches its end, a StopIteration exception is thrown indicating that the 
given generator has no more values. 

As a result, even though both functions must, in the end, do the same number of calculations, the range version of the 
preceding loop uses 10x more memory (or  Nx more memory if we are ranging from 1 to  N).

## Iterate over a pair of lists
```
lists = [(l1,l2) for l1 in list1 for l2 in list2 ]

lists = zip(list1,list2)
```

```
numbers = [1, 2, 3]
letters = ["A", "B", "C"]

for index in range(len(numbers)):
    print numbers[index], letters[index]
    
numbers = [1, 2, 3]
letters = ["A", "B", "C"]

for numbers_value, letters_value in zip(numbers, letters):
    print numbers_value, letters_value
```

>> Use izip to replace zip may be better

## List comprehension vs generator comprehension
A Generator Expression is doing basically the same thing as a List Comprehension does, but the GE does it lazily.

```
l = [n*2 for n in range(1000)] # List comprehension
g = (n*2 for n in range(1000))  # Generator expression
```

The size of used memory will reduce for generator version, however, we can not index it. It has beneficial in sum(), max(), etc 
as mentioned in ![PEP289](https://www.python.org/dev/peps/pep-0289/)
