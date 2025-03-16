---
title: "Python"
description: ""
summary: ""
date: 2024-10-18T20:27:56+08:00
lastmod: 2024-10-18T20:27:56+08:00
weight: 304
draft: false
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

### Python Tools

| Tools | Description |
| -------- | -------- |
| Python Intepreter | Python version that changes source code into machine language |
| Pip | Package manager for Python |
| Jupyter notebook (Ipython)| Can use browser to login into server and an IDE for python|
| Anaconda          | Manage python enviroments |
| Google Colab      | Run python notebook online with integrated IaaS, SaaS |
| Pycharm           | IDE suitable for web developement (High-Mid Scale) |
| Spyder            | IDE suitable for machine learning, deep learning (Mid-Low Scale) |

{{< details "Python Tools Details" >}}

#### Commands

```bash
python --version  # Show python version
python            # Run python intepreter
python script.py  # Run python script
pip install numpy # Install package
pip list          # List installed package
```

#### Jupyter Notebook Keyboard Shortcuts

| Keyboard Shortcuts | Description |
| -------- | -------- |
| `Shift + Enter` | Run current cell and move to next cell  |
| `Ctrl + Enter` | Run current cell |
| `II` | Interrupt  |
| `DD` | delete current cell |
| `A` | add new cell below |
| `B` | add new cell below |
| `C` | copy cell |
| `V` | paste cell |
| `Shift + M` | merge with below cell |

#### Anaconda

A tool to control python environment.

Commands

```bash
conda create --name envtest1 python=3.10  # Creating environment
conda create --name envtest2 python=3.11

conda activate envtest1           # Activate an environment
conda deactivate                  # Deactivate environment
conda env remove --name envtest1  # Remove environment

conda install numpy  # Is the same as `pip intall numpy`
conda list           # List installed package
conda env list       # List environments
where python         # Show which version of python the system is using
```

1. Don't set anaconda as global unless needed
2. Running cmd prompt will use system default python intepreter
3. Running anaconda prompt will use anaconda python intepreter
4. On VS Code, use `ctrl+shift+p` and choose 'Python: Select Intepreter' to change intepreter

{{< /details >}}


### Advanced Syntax

{{< details "Advanced Syntax" >}}

#### Common

```py
# Multiple assignments
a, b, c = 1, 2, 3

# Anonymous function
square = lambda x: x * x

# Using lambda in built-in functions
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x * x, numbers))  # [1, 4, 9, 16, 25]
even_nums = list(filter(lambda x: x % 2 == 0, numbers))  # [2, 4]

# Basic decorator
def my_decorator(func):
    def wrapper():
        print("Something before the function call")
        func()
        print("Something after the function call")
    return wrapper

# Using the decorator
@my_decorator
def say_hello():
    print("Hello!")

# Decorators with arguments
def repeat(n):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for _ in range(n):
                result = func(*args, **kwargs)
            return result
        return wrapper
    return decorator

@repeat(3)
def greet(name):
    print(f"Hello {name}")
```

#### Class

```py
class Employee(Person):
    # Constructor with parent's fields and new fields
    def __init__(self, name, age, employee_id):
        # Call parent's constructor
        super().__init__(name, age)
        self.employee_id = employee_id
    
    # Override parent's method
    def greet(self):
        return f"{super().greet()} and I work here"

# Multiple inheritance
class Student(Person):
    def __init__(self, name, age, student_id):
        super().__init__(name, age)
        self.student_id = student_id

class TeachingAssistant(Employee, Student):
    def __init__(self, name, age, employee_id, student_id):
        Employee.__init__(self, name, age, employee_id)
        self.student_id = student_id
```

#### Data Structure

```py {title="List"}
# Creating lists
fruits = ["apple", "banana", "cherry"]
numbers = list(range(1, 6))  # [1, 2, 3, 4, 5]

# Accessing elements
first_fruit = fruits[0]  # apple
last_fruit = fruits[-1]  # cherry

# Slicing
subset = fruits[1:3]  # ["banana", "cherry"]
first_two = fruits[:2]  # ["apple", "banana"]
last_two = fruits[-2:]  # ["banana", "cherry"]
every_second = fruits[::2]  # ["apple", "cherry"]
reversed_list = fruits[::-1]  # ["cherry", "banana", "apple"]

# List operations
fruits.append("orange")  # Add to end
fruits.insert(1, "kiwi")  # Insert at position
combined = fruits + ["grape", "mango"]  # Concatenation
fruits.remove("banana")  # Remove item
popped = fruits.pop()  # Remove and return last item
popped_index = fruits.pop(1)  # Remove and return at index

# List comprehensions
squares = [x**2 for x in range(10)]
even_squares = [x**2 for x in range(10) if x % 2 == 0]

lst = [1, 2, 3, 4, 5]
lst.append(6)              # Add item to the end
lst.extend([7, 8])         # Add multiple items to the end
lst.insert(0, 0)           # Insert item at position
lst.remove(3)              # Remove first occurrence of item
lst.pop()                  # Remove and return last item
lst.pop(0)                 # Remove and return item at index
lst.clear()                # Remove all items
lst.index(4)               # Find index of first occurrence
lst.count(2)               # Count occurrences
lst.sort()                 # Sort in place
lst.reverse()              # Reverse in place
sorted_lst = sorted(lst)   # Return a new sorted list
```

```py {title="Dictionary"}
# Creating dictionaries
person = {"name": "John", "age": 30, "city": "New York"}
another_dict = dict(name="Alice", age=25)

# Accessing values
name = person["name"]  # Error if key doesn't exist
age = person.get("age")  # Returns None if key doesn't exist
age = person.get("age", 0)  # Returns 0 if key doesn't exist

# Modifying dictionaries
person["email"] = "john@example.com"  # Add new key-value pair
person.update({"phone": "123-456-7890", "age": 31})  # Update multiple
del person["city"]  # Remove a key-value pair
phone = person.pop("phone")  # Remove and return value

# Dictionary comprehensions
squares = {x: x**2 for x in range(6)}  # {0:0, 1:1, 2:4, 3:9, 4:16, 5:25}

d = {'a': 1, 'b': 2}
d.keys()                   # View of keys
d.values()                 # View of values
d.items()                  # View of key-value tuples
d.get('c', 0)              # Get with default
d.setdefault('c', 3)       # Get key or set default if missing
d.update({'c': 3, 'd': 4}) # Update multiple keys
d.pop('b')                 # Remove and return value
d.popitem()                # Remove and return last key-value pair
d.clear()                  # Remove all items
```

```py {title="Set"}
# Creating sets
fruits = {"apple", "banana", "cherry"}
numbers = set([1, 2, 3, 2, 1])  # {1, 2, 3}

# Set operations
fruits.add("orange")  # Add item
fruits.remove("banana")  # Remove item (raises error if not found)
fruits.discard("kiwi")  # Remove item (no error if not found)

# Set operations
set1 = {1, 2, 3}
set2 = {3, 4, 5}
union = set1 | set2  # {1, 2, 3, 4, 5}
intersection = set1 & set2  # {3}
difference = set1 - set2  # {1, 2}
symmetric_diff = set1 ^ set2  # {1, 2, 4, 5}

# Set comprehensions
even_set = {x for x in range(10) if x % 2 == 0}  # {0, 2, 4, 6, 8}

s = {1, 2, 3}
s.add(4)                   # Add item
s.update([4, 5, 6])        # Add multiple items
s.remove(3)                # Remove item (raises error if missing)
s.discard(3)               # Remove item (no error if missing)
s.pop()                    # Remove and return arbitrary item
s.clear()                  # Remove all items
s.issubset({1, 2, 3, 4})   # Test if subset
s.issuperset({1, 2})       # Test if superset
s.isdisjoint({5, 6})       # Test if no common elements
```

#### File  IO

```py
# Basic file reading
with open("file.txt", "r") as file:
    content = file.read()  # Read entire file

# Reading line by line
with open("file.txt", "r") as file:
    for line in file:
        print(line.strip())

# Reading all lines at once
with open("file.txt", "r") as file:
    lines = file.readlines()  # Returns a list of lines

    # Writing to a file
with open("output.txt", "w") as file:
    file.write("Hello, World!")

# Appending to a file
with open("output.txt", "a") as file:
    file.write("\nAppended line")

# Writing multiple lines
lines = ["Line 1", "Line 2", "Line 3"]
with open("output.txt", "w") as file:
    file.writelines([line + "\n" for line in lines])
```

#### Error Handling

```py
# Basic try-except
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero")

# Multiple exceptions
try:
    num = int("abc")
except ValueError:
    print("Invalid conversion")
except (TypeError, ZeroDivisionError):
    print("Another error occurred")

# try-except-else-finally
try:
    file = open("file.txt", "r")
except FileNotFoundError:
    print("File not found")
else:
    content = file.read()  # Runs if no exception
    file.close()
finally:
    print("This always executes")  # Cleanup code
```

#### Modules

```py
# Basic try-except
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero")

# Multiple exceptions
try:
    num = int("abc")
except ValueError:
    print("Invalid conversion")
except (TypeError, ZeroDivisionError):
    print("Another error occurred")

# try-except-else-finally
try:
    file = open("file.txt", "r")
except FileNotFoundError:
    print("File not found")
else:
    content = file.read()  # Runs if no exception
    file.close()
finally:
    print("This always executes")  # Cleanup code
```

{{< /details >}}

### Libraries

#### Numpy

Library for numerical computing in Python.

{{< details "Numpy" >}}

```py
import numpy as np

# Basic 

a = np.array([2, 3, 4])         # Output: [2, 3, 4]
a = np.zeros((3, 2))            # Output: [[0. 0.], [0. 0.], [0. 0.]]
a = np.ones((2, 3), dtype=float)# Output: [[1. 1.], [1. 1.], [1. 1.]]
a = np.arange(3)                # Output: [0, 1, 2]
a = np.arange(10, 30, 5)        # Output: [10 15 20 25]
a = np.arange(6).reshape(3, 2)  # Output: [[0, 1], [2, 3], [4, 5]]
a = np.arange(6).reshape(3, -1) # Output: [[0, 1], [2, 3], [4, 5]], Automated
a = np.linspace(0, 2, 9)        # Output: [0. 0.25 0.5 0.75 1. 1.25 1.5 1.75 2.]
a = np.random.random((2, 1))    # Output: [[0.79498573], [0.22507543]] 

a = np.array( [[1,1],[0,1]] )
b = np.array( [[2,0],[3,4]] )
print(a + b)                    # Elementwise addition
print(a * b)                    # Elementwise product
print(np.sin(a))                # Radian sine to each element
print(np.cos(a))                # Radian cosine to each element
print(np.exp(a))                # Exponential to each element
print(np.sqrt(a))               # Square root to each element
print(np.dot(a, b))             # Matrix product
print(np.concatenate((a, b)))   # Concatenate
print(a is b)                   # True if both have exactly the same element

# Indexing and Iterating
a = np.arange(10) ** 2
print(a[-1])    # Last element
print(a[2:5])   # Element indexed 2 to 4
print(a[::-1])  # Reverse iteration
a[:6:2] = 1000  # Set every 2nd element to 1000
print(a)
b = np.array([1,3,5,7,9])
print(a[b])     # Elements indexed by b


# Multidimentional Array
def f(x, y):
    return 10 * x + y
a = np.fromfunction(f, (5, 4), dtype=int)
print(a)
print(a[0:5, 1])  # Each row in the second column of a
print(a[1:3, :])  # Each column in the second and third row of a

# Dots (...)
a = np.arange(12).reshape(2,2,3)
print(a)
print(a[1, ...])  # Output: [[ 6  7  8][ 9 10 11]].Same as c[1, :, :] or c[1]
print(a[..., 2])  # Output: [[ 2  5] [ 8 11]]. Same as c[:, :, 2]

for element in a.flat:  # Iterate over all elements instead of array entries
    print(element, end=' ')
print('\n', a.ravel())  # Flatten the array

a = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
print(a.ndim)       # Number of dimensions
print(a.shape)      # Shape of the array
print(a.size)       # Number of elements
print(a.dtype)      # Data type
print(a.itemsize)   # Size of each element
print(a.nbytes)     # Total size of the array

# Stacking Array
a = np.array([[1, 2], [3, 4]])
b = np.array([[5, 6], [7, 8]])
print(np.vstack((a, b)))  # Output: [[1 2][3 4][5 6][7 8]], same as np.row_stack((a, b))
print(np.hstack((a, b)))  # Output: [[1 2 5 6][3 4 7 8]], same as np.column_stack((a, b))
print(np.r_[a[0], b[0], 1:3, 8])    # Output: [1 2 5 6 1 2 8]
print(np.c_[a[0], b[0], 7:9])       # Output: [[1 2 5 6][3 4 7 8]]

# Splitting Array
a = np.array([[0, 1, 2, 3], [4, 5, 6, 7]])
b = np.arange(8, 0, -1).reshape(2, 4)
print(a)
print(b)

print(np.hsplit(a, 2))  # Split each row into 2 array
# Output: [array([[0, 1],[4, 5]]), array([[2, 3], [6, 7]])]

print(np.hsplit(a, (1, 3)))  # Split a at column 2 and 5
# Output: [array([[0], [4]]), array([[1, 2], [5, 6]]), array([[3], [7]])]

print(np.vsplit(a, 2))  # Split each column into 2 array
# Output: [array([[0, 1, 2, 3]]), array([[4, 5, 6, 7]])]

# Matrix
from numpy import matrix
from numpy import linalg

a = matrix('1 2 3; 4 5 6; 7 8 0')
b = matrix('1; 2; 3')
print(a * a)                # Matrix multiplication
print(a.T)                  # Transpose
print(linalg.det(a))        # Determinant 
print(linalg.inv(a))        # Inverse
print(linalg.pinv(a))       # Pseudo-inverse
print(linalg.solve(a, b))   # Solve linear system
```

{{< /details >}}

#### Pandas

Library for data manipulation and analysis in Python.

{{< details "Pandas" >}}

- Series: a one-dimensional labeled array holding data of any type
- DataFrame: a two-dimensional data structure

```py
import pandas as pd

s = pd.Series([1, 3, np.nan, "HI"])
print(s)

dates = pd.date_range("20130101", periods=6)
print(dates)
dates

df = pd.DataFrame(np.random.randn(6, 4), index=dates, columns=s)
print(df)
print(df.index)
print(df.columns)

df2 = pd.DataFrame(
    {
        "A": 1.0,
        "B": pd.Timestamp("20130102"),
        "C": pd.Series(1, index=list(range(4)), dtype="float32"),
        "D": np.array([3] * 4, dtype="int32"),
        "E": pd.Categorical(["test", "train", "test", "train"]),
        "F": "foo",
    }
)
print(df2)
print(df2.dtypes)
```

```py {title="Basic Operations"}
df.head()   # First 5 rows
df.tail()   # Last 5 rows
df.index    # Show index
df.columns  # Show columns
df.values   # Show values
df.describe()  # Summary
df.T        # Transpose
df.sort_index(axis=1, ascending=False)  # Sort by index
df.sort_values(by="B")  # Sort by column B
df.to_numpy()  # Convert to numpy
df["New_col"] = pd.Series([1, 2, 3, 4, 5, 6])   # Add new column
```

```py {title="Selection"}
dates = pd.date_range("20130101", periods=6)
df = pd.DataFrame(np.random.randn(6, 4), index=dates, columns=list("ABCD"))
df["D"] = ["one", "one", "two", "three", "four", "three"]

print(df)
print(df["A"])      # Getitem
print(df[0:3])      # Row 1 to 3
print(df["20130102":"20130104"])
print(df.loc[dates[0]])     # Selecting a row matching label
print(df.loc[:,["A", "B"]]) # Selecting all row with column A and B
print(df.iloc[1:3, 0:2])    # Selecting row 3 to 5 and column 0 to 2 by index
print(df[df["A"] > 0])      # Select rows where df.A is greater than 0
print(df[df["D"].isin(["two", "four"])])
print(df.at[dates[0], "A"])  # Selecting a first element
print(df.iat[0, 0])          # Selecting a first element
```

```py {title="Missing Data"}
dates = pd.date_range("20130101", periods=6)
df = pd.DataFrame(np.random.randn(6, 4), index=dates, columns=list("ABCD"))

df.dropna(how="any")    # Drop rows with missing data
df.fillna(value=0)      # Fill missing data with 0
print(pd.isna(df))      # Return boolean mask where data is missing
```

```py {title="Operations"}
dates = pd.date_range("20130101", periods=6)
df = pd.DataFrame(np.random.randn(6, 4), index=dates, columns=list("ABCD"))
s = pd.Series([1, 3, 5, np.nan, 6, 8], index=dates).shift(2)
print(s)
t = pd.Series(np.random.randint(0, 7, size=10))
print(t)

df.mean()               # Mean for each column
df.mean(axis=1)         # Mean for each row
df.add(s, axis="index") # Add series to dataframe at index
# df.agg("User defined function")
# df.transform("User defined function")
t.value_counts()        # Show frequency of each element

pieces = [t[:3], t[3:7], t[7:]]  # Break into piece
pd.concat(pieces)                # Concatenate
```

```py {title="Merge"}
left = pd.DataFrame({"key": ["foo", "foo"], "lval": [1, 2]})
right = pd.DataFrame({"key": ["foo", "foo"], "rval": [4, 5]})
print(pd.merge(left, right, on="key"))

left = pd.DataFrame({"key": ["foo", "bar"], "lval": [1, 2]})
right = pd.DataFrame({"key": ["foo", "bar"], "rval": [4, 5]})
print(pd.merge(left, right, on="key"))
```

```py {title="Grouping"}
df = pd.DataFrame(
    {
        "A": ["foo", "bar", "foo", "bar", "foo", "bar", "foo", "foo"],
        "B": ["one", "one", "two", "three", "two", "two", "one", "three"],
        "C": np.random.randn(8),
        "D": np.random.randn(8),
    }
)

print(df.groupby("A")[["C", "D"]].sum())
print(df.groupby(["A", "B"]).sum())
```

```py {title="Stack"}
arrays = [
   ["bar", "bar", "baz", "baz", "foo", "foo", "qux", "qux"],
   ["one", "two", "one", "two", "one", "two", "one", "two"],
]
index = pd.MultiIndex.from_arrays(arrays, names=["first", "second"])
df = pd.DataFrame(np.random.randn(8, 2), index=index, columns=["A", "B"])

print(df)
print(df.stack(future_stack=True))
print(df.unstack())
print(df.unstack(1))
print(df.unstack(0))
```

```py {title="CSV"}
df = pd.DataFrame(np.random.randint(0, 5, (10, 5)))

df.to_csv("foo.csv")
pd.read_csv("foo.csv")

df.to_excel("foo.xlsx", sheet_name="Sheet1")
pd.read_excel("foo.xlsx", "Sheet1", index_col=None, na_values=["NA"])
```

{{< /details >}}

#### Matplotlib

Library for creating static, animated, and interactive visualizations in Python.

{{< details "Matplotlib" >}}

```py
%matplotlib inline  # Allow notebook to display plots
import matplotlib.pyplot as plt
import numpy as np

x = [1, 2, 3, 4, 5]
y = [10, 16, 4, 8, 6]
y1 = [1, 2, 3, 4, 5]
y2 = [5, 4, 3, 2, 1]

plt.plot(x, y, label='a', color='b', linestyle='-', marker='o')
plt.plot(x, y1, label='b', color='r', linestyle='-', marker='o') 
plt.plot(x, y2, label='c', color='g', linestyle='-', marker='o')
plt.xlabel('Label X-Axis')
plt.ylabel('Label Y-Axis')
plt.title('Title of Plot')
plt.legend(loc='upper left', fontsize='small', frameon=True, title='Legend Title')
plt.show()
```

```py {title="Colormaps"}
import matplotlib.pyplot as plt
import numpy as np
from matplotlib.collections import LineCollection

x = np.linspace(0, 10, 100)
y = np.sin(x)
segments = []
for i in range(len(x) - 1):
    segments.append([(x[i], y[i]), (x[i + 1], y[i + 1])])
cmap = plt.cm.get_cmap('cool')
lc = LineCollection(segments, cmap=cmap)
lc.set_array(x)
fig, ax = plt.subplots()
ax.add_collection(lc)
ax.autoscale()
plt.show()

x = [1, 2, 3, 4, 5]
y = ["a", "b", "c", "d", "e"]
fig, ax = plt.subplots()
ax.pie(x, labels = y)
plt.show()
```

```py {title="Subplots"}
x = [1, 2, 3, 4, 5]
y = [10, 16, 4, 8, 6]

fig, axs = plt.subplots(2, 2)
axs[0, 0].plot(x, y)
axs[0, 1].scatter(x, y)
axs[1, 0].bar(x, y)
axs[1, 1].hist(y)
plt.show()
```

```py {title="Pandas Plot"}
df = pd.DataFrame(
    np.random.randn(1000, 4), index=pd.date_range("1/1/2000", periods=1000), columns=["A", "B", "C", "D"]
)

df = df.cumsum()
plt.figure()
df.plot()
plt.legend(loc='best')
```

{{< /details >}}

#### Seaborn

Library for making statistical graphics in Python.

{{< details "Seaborn" >}}

{{< /details >}}

#### Scikit-learn

Library for machine learning in Python.

#### Tensorflow

Library for deep learning in Python. Developed by Google.

#### PyTorch

Library for machine learning in Python. Developed by Facebook.

#### Keras

Library for deep learning in Python. Developed by Google.

#### Tkinter

Library for GUI development in Python.

