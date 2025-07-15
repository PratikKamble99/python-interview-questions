## 1. How Python is interpreted?
1. Python as a language is not interpreted or compiled. Interpreted or compiled is the property of the implementation. Python is a bytecode(set of interpreter readable instructions) interpreted generally.
Source code is a file with .py extension.
2. Python compiles the source code to a set of instructions for a virtual machine. The Python interpreter is an implementation of that virtual machine. This intermediate format is called “bytecode”.
3. `.py` source code is first compiled to give .pyc which is bytecode. This bytecode can be then interpreted by the official CPython or JIT(Just in Time compiler) compiled by PyPy.


## 2. What are Comprehensions in Python?
Comprehensions in Python provide a concise way to create collections like `lists, sets, or dictionaries` using a single line of code.
1. Performing mathematical operations on the entire list
```python 
my_list = [2, 3, 5, 7, 11]
squared_list = [x**2 for x in my_list]    # list comprehension
# output => [4 , 9 , 25 , 49 , 121]
squared_dict = {x:x**2 for x in my_list}    # dict comprehension
# output => {11: 121, 2: 4 , 3: 9 , 5: 25 , 7: 49}
```
2. Performing conditional filtering operations on the entire list
```python 
my_list = [2, 3, 5, 7, 11]
squared_list = [x**2 for x in my_list if x%2 != 0]    # list comprehension
# output => [9 , 25 , 49 , 121]
squared_dict = {x:x**2 for x in my_list if x%2 != 0}    # dict comprehension
# output => {11: 121, 3: 9 , 5: 25 , 7: 49}
```
3. Combining multiple lists into one
```python
a = [1, 2, 3]
b = [7, 8, 9]
[(x + y) for (x,y) in zip(a,b)]  # parallel iterators
# output => [8, 10, 12]

[(x,y) for x in a for y in b]    # nested iterators
# output => [(1, 7), (1, 8), (1, 9), (2, 7), (2, 8), (2, 9), (3, 7), (3, 8), (3, 9)] 
```
4. Flattening a multi-dimensional list
```python
my_list = [[10,20,30],[40,50,60],[70,80,90]]
flattened = [x for temp in my_list for x in temp]
# output => [10, 20, 30, 40, 50, 60, 70, 80, 90]
```


## 3. What are Decorators in Python?
A decorator in Python is a function that `modifies the behavior of another function or method` — without changing its code. It's a powerful tool for code reuse, logging, access control, timing, and more.
```python
# decorator function to convert to lowercase
def lowercase_decorator(function): # function =  hello
   def wrapper():
       func = function() # hello () --> return "Hello World"
       string_lowercase = func.lower() 
       return string_lowercase # "hello world"
   return wrapper

# decorator function to split words
def splitter_decorator(function): # function = lowercase_decorator
   def wrapper():
       func = function() # lowercase_decorator() --> return "hello world"
       string_split = func.split()
       return string_split # [ 'hello' , 'world' ]
   return wrapper

@splitter_decorator # this is executed next
@lowercase_decorator # this is executed first
def hello():
   return 'Hello World'
hello()   # output => [ 'hello' , 'world' ]

# same as
lowercase_and_split = lowercase_decorator(splitter_decorator(hello))
lowercase_and_split()
```

## 4. Scope Resolution in Python
Scope Resolution in Python refers to `how Python determines where to look for a variable` — whether it's local, enclosing, global, or built-in. Python follows the LEGB Rule to resolve the scope.

```python
temp = 10   # global-scope variable
def func():
     temp = 20   # local-scope variable
     print(temp)
print(temp)   # output => 10
func()    # output => 20
print(temp)   # output => 10
```
1. global — Access/modify global variable inside a function
```python
temp = 10   # global-scope variable
def func():
     global temp
     temp = 20   # local-scope variable
     print(temp)
print(temp)   # output => 10
func()    # output => 20
print(temp)   # output => 20

```
2. nonlocal — Modify a variable in the enclosing (non-global) function
```python 
def outer():
    count = 0
    def inner():
        nonlocal count
        count += 1
        print(count)
    inner()

outer()
```

## 5. Namespace in Python
A namespace in Python is a container that holds names (identifiers) like variable names, function names, class names, etc., and maps them to their corresponding objects (values or functions).
| Namespace     | Description                                       | Lifetime                               |
| ------------- | ------------------------------------------------- | -------------------------------------- |
| **Built-in**  | Contains names like `len()`, `str`, `int`, etc.   | Exists as long as Python is running    |
| **Global**    | Created when a module/script is run               | Until script/module ends               |
| **Enclosing** | For outer functions in nested functions           | As long as the outer function is alive |
| **Local**     | Inside a function — contains local variable names | Until the function finishes execution  |

## 6. memory managed in Python
1. Memory management in Python is handled by the `Python Memory Manager`. The memory allocated by the manager is in `form of a private heap space` dedicated to Python. All Python objects are stored in this heap and being private, it is inaccessible to the programmer. Though, python does provide some core API functions to work upon the private heap space.
2. Additionally, Python has an `in-built garbage collection` to recycle the unused memory for the private heap space.

## 7. What is lambda in Python? Why is it used?
Lambda is an anonymous function in Python, that can accept any number of arguments, but it `alwyas have a single expression`.
```python
mul = lambda a, b : a * b
print(mul(2, 5))    # output => 10
```

## 8. *args and **kwargs
`*args` and `**kwargs` are used in function definitions to allow variable-length arguments — giving your functions flexibility to accept any number of positional and keyword arguments.

```python
def print_numbers(*args):  # this extracts individual arguments into list
    # args = [1, 2, 3, 4, 5, 6]
    for i in args:         # this also called positional arguments
        print(i)

print_numbers(1, 2, 3, 4, 5, 6)
```
```python
def print_details(**kwargs): # this extracts arguments into key-value pair
    # kwargs = {'name':'pratik', 'age':20}
    for key,value in kwargs.items():
        print(f"{key}:{value}")

print_details(name="pratik", age=20) # this converts into dictionary
``` 

## 9. What is an Iterator?
An iterator in Python is an object that allows you to `traverse through a sequence of elements, one item at a time`.
```
 It implements two special methods:
__iter__()    # Returns the iterator object itself
__next__()    # Returns the next value from the sequence
```

```python
nums = [1, 2, 3]

# Turn it into an iterator
it = iter(nums)

print(next(it))  # 1
print(next(it))  # 2
print(next(it))  # 3
```

```python
# Custom Iterator Class
class Counter:
    def __init__(self, start, end):
        self.current = start
        self.end = end

    def __iter__(self):
        return self

    def __next__(self):
        if self.current > self.end:
            raise StopIteration
        self.current += 1
        return self.current - 1

c = Counter(1, 3)
for num in c:
    print(num)
```

## 10. passed by value or by reference in python
1. Pass by value: Copy of the actual object is passed. Changing the value of the copy of the object will not change the value of the original object.
2. Pass by reference: Reference to the actual object is passed. Changing the value of the new object will change the value of the original object.

```
Immutable objects (e.g., int, float, str, tuple) behave like pass-by-value.

Mutable objects (e.g., list, dict, set, custom objects) behave like pass-by-reference.
```
```python 
def appendNumber(arr):
   arr.append(4)
arr = [1, 2, 3]
print(arr)  #Output: => [1, 2, 3]
appendNumber(arr)
print(arr)  #Output: => [1, 2, 3, 4]
```

## 11. What is generator?

Generators are functions that return an iterable collection of items, one at a time, in a set manner.                
Generators, in general, are used to create iterators with a different approach. They employ the use of yield keyword rather than return to return a generator object.
```python
## generate fibonacci numbers upto n
def fib(n):
   p, q = 0, 1
   while(p < n):
       yield p
       p, q = q, p + q
x = fib(10)    # create generator object 
 
## iterating using __next__(), for Python2, use next()
x.__next__()    # output => 0
x.__next__()    # output => 1
x.__next__()    # output => 1
x.__next__()    # output => 2
x.__next__()    # output => 3
x.__next__()    # output => 5
x.__next__()    # output => 8
x.__next__()    # error
 
## iterating using loop
for i in fib(10):
   print(i)    # output => 0 1 1 2 3 5 8
```

## 12. Pickling vs Unpickling
1. What is Pickling?                               
Pickling is the process of serializing a Python object — converting it into a byte stream that can be saved to a file or sent over a network.

```python 
import pickle

data = {'name': 'Alice', 'age': 25}

# Serialize and save to file
with open('data.pkl', 'wb') as f:
    pickle.dump(data, f)
```

**Picklable**:
Built-in types (list, dict, int, str, etc.), Functions and classes defined at the top level,Custom class instances (if not using non-picklable resources)

**Not Picklable**:
Open file objects, 
Sockets, database connections, 
Lambda functions or local functions

2. What is Unpickling?      
Unpickling is the process of deserializing the byte stream back into a Python object.

```python
import pickle

# Load from file and deserialize
with open('data.pkl', 'rb') as f:
    loaded_data = pickle.load(f)

print(loaded_data)  # {'name': 'Alice', 'age': 25}
```

## 13. Shallow vs Deep copy
1. Shallow Copy (copy.copy()):

    Creates a new object, but copies references to the original inner objects.
    Changes to nested objects affect both the original and the copy.

    ```python
    import copy

    original = [1, 2, [3, 4]]
    shallow = copy.copy(original)

    shallow[2][0] = 99
    print(original)  # Output: [1, 2, [99, 4]]
    ```
2. Deep Copy (copy.deepcopy()):

    Creates a new object and recursively copies all nested objects.Original and copied objects are fully independent.

    ```python
    import copy

    original = [1, 2, [3, 4]]
    deep = copy.deepcopy(original)

    deep[2][0] = 99
    print(original)  # Output: [1, 2, [3, 4]]
    print(deep)      # Output: [1, 2, [99, 4]]
    ```

## 14.Why is __del__() or finalize used in Python?
In Python, finalization is the process of performing cleanup actions when an object is about to be destroyed (i.e., garbage collected). This is typically done using:

```python 
## __del__() Method (Destructor)
## You can use it to close files, release resources, or log destruction.

class MyClass:
    def __del__(self):
        print("Object is being destroyed")

obj = MyClass()
del obj  # Triggers __del__()
```

```python
## weakref.finalize() (Preferred for cleanup)
## Used to register a cleanup function when an object is garbage collected.

import weakref

class Resource:
    def close(self):
        print("Resource closed")

res = Resource()
weakref.finalize(res, res.close)
del res  # "Resource closed" will be printed
```

## 15. access parent members in the child class
1. By using Parent class name: You can use the name of the parent class to access the attributes as shown in the example below:

```python 
class Parent(object):  
   # Constructor
   def __init__(self, name):
       self.name = name    
 
class Child(Parent): 
   # Constructor
   def __init__(self, name, age):
       Parent.name = name
       self.age = age
 
   def display(self):
       print(Parent.name, self.age)
 
# Driver Code
obj = Child("Interviewbit", 6)
obj.display()
```

2. By using super(): The parent class members can be accessed in child class using the super keyword.

```python
class Parent(object):
   # Constructor
   def __init__(self, name):
       self.name = name    
 
class Child(Parent):
   # Constructor
   def __init__(self, name, age):         
       ''' 
       In Python 3.x, we can also use super().__init__(name)
       ''' 
       super(Child, self).__init__(name)
       self.age = age
 
   def display(self):
      # Note that Parent.name cant be used 
      # here since super() is used in the constructor
      print(self.name, self.age)
  
# Driver Code
obj = Child("Interviewbit", 6)
obj.display()
```
