##Exception Handling, File I/O, Logging & Memory Management
### Theoretical Concepts

#### What is the difference between interpreted and compiled languages?

* **Interpreted languages** (e.g., Python): Code is executed line by line by an interpreter at runtime.
* **Compiled languages** (e.g., C, Java): Code is converted into machine code ahead of time using a compiler.

#### What is exception handling in Python?

Exception handling lets you manage runtime errors using:

* `try`: Code that may raise an exception
* `except`: Handle exceptions
* `else`: Executes if no exception occurs
* `finally`: Executes regardless of exceptions (for cleanup)

#### Purpose of the `finally` block?

It runs **regardless of whether an exception occurred** — useful for resource cleanup, such as closing files.

#### What is logging in Python?

Logging tracks events and errors during execution. Python’s `logging` module lets you log messages to console, files, or external systems using levels like `INFO`, `ERROR`, etc.

#### What is the `__del__()` method?

This is a destructor in Python. It's called when an object is about to be destroyed. Used to release resources, such as file handles or network connections.

#### `import` vs `from ... import`

* `import module`: Import entire module (access via `module.name`)
* `from module import name`: Import specific name directly

#### How to handle multiple exceptions?

Either:

```python
try:
    ...
except (TypeError, ValueError):
    ...
```

Or use multiple `except` blocks for specific exception types.

#### Purpose of `with` statement in file handling?

Automatically manages file resources. It ensures the file is **properly closed**, even if an error occurs.

#### Multithreading vs Multiprocessing

| Feature  | Multithreading             | Multiprocessing                       |
| -------- | -------------------------- | ------------------------------------- |
| Memory   | Shared memory              | Separate memory                       |
| Use case | I/O-bound tasks            | CPU-bound tasks                       |
| Speedup  | Context switching overhead | True parallelism using multiple cores |

#### Benefits of using logging

* Tracks program execution
* Helps in debugging and monitoring
* More flexible than print statements
* Supports log levels and file output

#### What is memory management in Python?

* Automatic garbage collection
* Reference counting and cyclic garbage detection
* Manages allocation and deallocation of memory for objects

#### Basic steps in exception handling

```python
try:
    # risky code
except ExceptionType:
    # handle error
else:
    # runs if no error
finally:
    # always runs (cleanup)
```

#### Why is memory management important?

Prevents:

* Memory leaks
* Excessive memory consumption
* Resource wastage

#### How does Python's garbage collection system work?

* Uses **reference counting**
* Detects and collects cyclic references
* Automatically frees memory when objects are no longer in use

#### What are the common logging levels?

* `DEBUG`, `INFO`, `WARNING`, `ERROR`, `CRITICAL`

#### `os.fork()` vs `multiprocessing`

* `os.fork()`: Unix-only, low-level child process creation
* `multiprocessing`: Cross-platform, higher-level parallel processing with safer resource handling

#### Importance of closing a file?

* Frees system resources
* Flushes data to disk
* Prevents file locks or corruption

#### `file.read()` vs `file.readline()`

* `read()`: Reads entire content at once
* `readline()`: Reads one line at a time

#### What is the `os` module used for?

Used to interact with the file system (navigate directories, rename/move/delete files, etc.)

#### Challenges in Python memory management

* Handling **circular references**
* Detecting **leaks in C extensions**
* Efficient cleanup of large/unused objects

#### How to manually raise an exception?

```python
raise ValueError("This is an error!")
```

#### When is multithreading important?

* When handling **I/O-bound tasks** such as file operations, API requests, etc.
* Improves responsiveness without parallel CPU usage

#### Open a file for writing and write a string

```python
with open('example.txt', 'w') as file:
    file.write("Hello, world!")
```

#### Read a file line by line

```python
with open('example.txt', 'r') as file:
    for line in file:
        print(line)
```

#### Handle file not found error

```python
try:
    with open('nonexistent.txt', 'r') as file:
        content = file.read()
except FileNotFoundError:
    print("File not found!")
```

#### Copy contents from one file to another

```python
with open('source.txt', 'r') as source_file:
    content = source_file.read()

with open('destination.txt', 'w') as dest_file:
    dest_file.write(content)
```

#### Handle division by zero error

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero!")
```

#### Read file lines into a list

```python
with open('example.txt', 'r') as file:
    lines = file.readlines()

print(lines)
```

#### Append data to a file

```python
with open('example.txt', 'a') as file:
    file.write("\nNew data added.")
```

#### Handle missing key in dictionary

```python
my_dict = {"a": 1, "b": 2}

try:
    value = my_dict['c']
except KeyError:
    print("Key not found!")
```

#### Multiple exception handling

```python
try:
    num = int(input("Enter a number: "))
    result = 10 / num
except ValueError:
    print("Invalid input!")
except ZeroDivisionError:
    print("Cannot divide by zero!")
```
#### Check if a file exists

```python
import os

if os.path.exists('example.txt'):
    with open('example.txt', 'r') as file:
        content = file.read()
else:
    print("File does not exist.")
```

#### Print file content or notify if it's empty

```python
try:
    with open('example.txt', 'r') as file:
        content = file.read()
        if content:
            print(content)
        else:
            print("The file is empty.")
except FileNotFoundError:
    print("File not found.")
```

#### Write list of numbers to a file (1 per line)

```python
numbers = [1, 2, 3, 4, 5]
with open('numbers.txt', 'w') as file:
    for number in numbers:
        file.write(f"{number}\n")
```

#### Memory profiling with `memory_profiler`

```python
import memory_profiler

@memory_profiler.profile
def my_function():
    a = [1] * (10**6)
    b = [2] * (2 * 10**7)
    del b
    return a

my_function()
```

#### Setup logging with file rotation after 1MB

```python
import logging
from logging.handlers import RotatingFileHandler

handler = RotatingFileHandler('logfile.log', maxBytes=1e6, backupCount=3)
logger = logging.getLogger()
logger.addHandler(handler)
logger.setLevel(logging.INFO)

logger.info("This is a log message.")
```

#### Handle `IndexError` and `KeyError`

```python
my_list = [1, 2, 3]
my_dict = {"a": 1, "b": 2}

try:
    print(my_list[5])
except IndexError:
    print("Index out of range!")

try:
    print(my_dict['c'])
except KeyError:
    print("Key not found!")
```

#### Read file with context manager

```python
with open('example.txt', 'r') as file:
    content = file.read()
    print(content)
```

#### Count word occurrences in a file

```python
word_to_search = "Python"
with open('example.txt', 'r') as file:
    content = file.read()
    count = content.lower().count(word_to_search.lower())
    print(f"The word '{word_to_search}' appears {count} times.")
```
