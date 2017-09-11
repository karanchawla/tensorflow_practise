# Functions
### Returning None
1. Functions that return None to indicate special meaning are error prone because None and other values(eg zero,empty string etc.) 
all evaluate to zero in conditionals. 
2. Raise exceptions instead to indicate special situations instead of returning None. Expect the calling code to handle exceptions.
3. eg: 

```
def divide(a,b):
    try:
        return (a/b)
    except ZeroDivisionError as e:
        raise ValueError('Invalid Inputs') from e
```

### Scope
4. Closure functions can refer to variables from any of the scopes in which they were defined. 
5. By default, closure can't affect enclosing scopes by assigning values. 
6. In Py3, use nonlocal statement to indicate when a closure can modify a variable in its enclosing scope. 
7. In Py2, use mutable value like a list to change the value of the variable. 
8. Avoid using nonlocal statements for aything other than simple functions. 
9. eg:

```
def sort_priority3(numbers, group):
	found =	False
	def	helper(x):
	nonlocal found
	if x in	group:
		found =	True
		return	(0,x)
	return	(1, x)
numbers.sort(key=helper)
return	found
```
Another way of achieving the same thing is to use define a class:
```
class SortPriority(object):
    def __init__(self,group):
        self.found = False
        self.group = group
    
    def __call__(self,x):
        if x in self.group:
            self.found = True
            return(0,x)
        return(1,x)
        
sorter = SortPriority(group)
numbers.sort(key=sorter) 
assert sorter.found is True
```

### Generators over Lists
10. Using generators can be clearer than the alternative of returning lists of accumulate results.
11. The iterator rturned by a generator produces the set of values passed to `yield` expressions within the generator function's
body. 
12. Generators can produce a sequence of outputs for arbitrarily large inputs because their working memory doesn't include all
the inputs and outputs. 
13. eg:

```
def index_to_words(text):
    if text:
        yield 0
    for index, letter in enumerate(text):
        if letter=' ':
            yield index + 1

results = list(index_to_words(text))
```

### Use Enumerate over Range
14. eg: 

```
for i, flavor in enumerate(flavor_list):
	print('%d: %s' %(i+1,flavor))
```
15. enumerate provides concise syntax for looping over an iterator and getting the index of each item from the iterator as you go. 

16. You can supply a second parameter to enumerate to specify the number from which to begin counting.(zero is default)

### Use zip to process iterators in parallel

17. eg: 

```
names = ['Jon', 'Danerys', 'Cersei']
letters = [len(n) for n in names]

for name, count in zip(names, letters):
	if count > max_letters:
	longest_name = name
	max_letters = count
```

18. zip built in finctions can be used to iterate over multiple iterators in parallel. 
19. zip truncates output silently if different size inputs are fed. 
20. zip_longest from itertools built in module lets you iterate over multplie iterators in parallel regardless of their lengths. 

21. Avoid else blocks after for and while loops. Python has special syntax that allows else blocks to immediately follow for and while loop interior blocks. 
22. The else block after a loop only runs if the loop body did not encounter a break statement. 
23. Avoid using else blocks after loops because their behavior isn't intuitive and can be confusing.  






























