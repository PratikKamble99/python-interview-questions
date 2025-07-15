## 1. What is `__init__()`
    
The `__init__` method in a Python class is known as the constructor. 
    It is automatically called when you create a new instance of a class. 
    Its primary role is to initialize the object’s attributes with values.

```python
class ClassName:
    def __init__(self, arguments):
    # initialization logic
```

## 2. Python array vs list

1. Arrays:- in python can only contain elements of same data types i.e., data type of array should be homogeneous. It is a thin wrapper around C language arrays and consumes far less memory than lists.

2. List:- in python can contain elements of different data types i.e., data type of lists can be heterogeneous. It has the disadvantage of consuming large memory.

```python
import array
a = array.array('i', [1, 2, 3])
for i in a:
    print(i, end=' ')    #OUTPUT: 1 2 3

a = array.array('i', [1, 2, 'string'])    #OUTPUT: ❌ TypeError: an integer is required (got type str)

a = [1, 2, 'string'] # list
for i in a:
   print(i, end=' ')    #OUTPUT: 1 2 string
```

## 3. What is Slicing?
Slicing in Python allows you to extract a portion (a "slice") of a list, string, or any sequence type using the syntax:

1. start: Index where the slice starts (inclusive)
2. stop: Index where the slice ends (exclusive)
3. step: Interval between elements (default is 1)
```
sequence[start:stop:step]
```
## 4. What is docstring in Python?
A docstring (documentation string) is a special string used to document Python modules, classes, functions, or methods.

A docstring (documentation string) is a special string used to document Python modules, classes, functions, or methods.

## 5. What is break, continue and pass in Python?
1. Break:-	The break statement terminates the loop immediately.

2. Continue:-	The continue statement terminates the current iteration of the statement, skips the rest of the code in the current iteration and the control flows to the next iteration of the loop.

3. Pass:-	The pass statement in Python is a null operation — it does nothing when executed. It's used as a placeholder in blocks of code where syntactically some code is required but you haven't written it yet.
```python
pat = [1, 3, 2, 1, 2, 3, 1, 0, 1, 3]
for p in pat:
   pass
   if (p == 0):
       current = p
       break
   elif (p % 2 == 0):
       continue
   print(p)    # output => 1 3 1 3 1
print(current)    # output => 0
```

## 6. Use of `self` in Python

The `self` keyword refers to the current instance of the class. It is automatically passed to instance methods and is used to access variables that belong to the class.

### Example:

```python
class Dog:
    def __init__(self, name, breed):
        self.name = name       # Instance variable
        self.breed = breed

    def bark(self):
        print(f"{self.name} says Woof!")

```
## 7. Global, Protected, and Private Attributes in Python:

| Access Type | Prefix     | Intended Access Scope          | Enforced? |
|-------------|------------|-------------------------------|-----------|
| Global      | *(None)*   | Anywhere in the module         | ✅        |
| Protected   | `_var`     | Class and subclasses only      | ❌ (by convention) |
| Private     | `__var`    | Only within the class          | ✅ (via name mangling) |

```python
class Person:
    def __init__(self, name, age, salary):
        self.name = name # public variable - can acces from anywhere
        self._age = age # protected variable - can acces from itself and derived class only
        self.__salary = salary # private variable - can acces from in same class only

class Employee(Person):
    def __init__(self, name, age, salary):
        super().__init__(name, age, salary)

pratik = Person('Pratik', 25, 700000)
print(pratik.name)
# print(pratik._age) # get error
# print(pratik.__salary) # get error

rutik = Employee('Rutik', 26, 100000 )

print(rutik._age) # will acces from subclass
```

## 8. Modules and Packages in Python
1.  module: A **module** is a single Python file (`.py`) that contains functions, classes, or variables which you can reuse in other Python programs.

**math_utils.py**
```python
def add(a, b):
    return a + b
```
**other-file.py**
```python
import math_utils
print(math_utils.add(3, 5))  # Output: 8
```


2. packages: A **package** is a directory that contains multiple modules and a special file called `__init__`.py.

```
my_package/
│
├── __init__.py
├── operations.py
└── utilities.py
```

**operations.py**
```python
def multiply(a, b):
    return a * b
```

**main.py**
```python
from my_package import operations

print(operations.multiply(2, 3))  # Output: 6
```

## 9. Data-types
```
| Category     | Data Type    | Example                            | Description                            |
|--------------|--------------|------------------------------------|----------------------------------------|
| Numeric      | `int`        | `x = 10`                           | Integer numbers                         |
|              | `float`      | `y = 3.14`                         | Decimal numbers                         |
|              | `complex`    | `z = 2 + 3j`                       | Complex numbers                         |
| Text         | `str`        | `name = "Alice"`                   | Sequence of Unicode characters          |
| Sequence     | `list`       | `fruits = ['apple', 'banana']`     | Ordered, mutable collection             |
|              | `tuple`      | `coords = (10, 20)`                | Ordered, immutable collection           |
|              | `range`      | `r = range(5)`                     | Sequence of numbers                     |
| Mapping      | `dict`       | `data = {'a': 1, 'b': 2}`          | Key-value pairs                         |
| Set          | `set`        | `s = {1, 2, 3}`                    | Unordered collection of unique items   |
|              | `frozenset`  | `fs = frozenset([1, 2, 3])`        | Immutable set                           |
| Boolean      | `bool`       | `flag = True`                      | Logical value: `True` or `False`        |
| None Type    | `NoneType`   | `x = None`                         | Represents null/empty value             |
```

## 10. What are Lists and Tuples in Python?
In Python, lists and tuples are both sequence types used to store collections of items — such as numbers, strings, or even other lists/tuples.

```
Feature	        List ([])	                Tuple (())
------------ ----------------------------- ----------------------------
Mutability	    ✅ Mutable	                ❌ Immutable
Syntax	        []	                        ()
Performance	    Slower (more flexible)	    Faster (more memory-efficient)
Methods	Many    (append, remove, etc.)	    Few (count, index)
Use Case	    Use when data can change    Use for fixed collections
```
```python
my_tuple = ('sara', 6, 5, 0.97)
my_list = ['sara', 6, 5, 0.97]
print(my_tuple[0])     # output => 'sara'
print(my_list[0])     # output => 'sara'
my_tuple[0] = 'ansh'    # modifying tuple => throws an error
my_list[0] = 'ansh'    # modifying list => list modified
print(my_tuple[0])     # output => 'sara'
print(my_list[0])     # output => 'ansh'
```

## 11. Types of Scope in Python
| Scope Type    | Description                                   | Example Area              |
| ------------- | --------------------------------------------- | ------------------------- |
| **Local**     | Inside the current function                   | Inside a function         |
| **Enclosing** | Inside outer functions (for nested functions) | Outer function in closure |
| **Global**    | At the top-level of a script or module        | Outside all functions     |
| **Built-in**  | Provided by Python (e.g., `len()`, `print()`) | Always accessible         |

```python
x = "global"

def outer():
    x = "enclosing"
    
    def inner():
        x = "local"
        print(x)  # prints 'local'
    
    inner()
    print(x)  # prints 'enclosing'

outer()
print(x)  # prints 'global'
```

## 12. An interpreted, dynamically typed, and strongly typed language
###  1. Interpreted Language

Python code is **executed line by line** by an interpreter at runtime, rather than being compiled into machine code beforehand.

### Example:

```python
print("Start")
x = 10 / 0      # Error occurs here
print("End")    # This line won't run
```

Only the lines before the error are executed. This helps in **easier debugging** and **quick testing**.

---

### 2. Dynamically Typed

Python **does not require you to declare variable types**. The type of a variable is determined at **runtime**, and can even change.

### Example:

```python
x = 5          # x is an int
x = "hello"    # now x is a str
```

There’s no need to specify `int` or `str`. This makes Python **flexible** but also requires developers to be careful with type usage.

---

###
  3. Strongly Typed

Although Python is dynamically typed, it is **strongly typed**, meaning it **does not allow implicit type conversion (type coercion)** that might lead to unexpected results.

### Example:

```python
print("1" + 2)  # ❌ TypeError: can only concatenate str (not "int") to str
```

In **weakly typed** languages like JavaScript, this would output `"12"` due to implicit conversion, but Python **raises an error** to avoid confusion.

---















