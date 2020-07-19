# Python Exception Tree

The [Programming Fundamentals in Python (Part 2)](https://edube.org/study/pe2) course has a very interesting example no 5.6.4. 

It prints the tree of Python standard library exceptions.

```Python
def PrintExcTree(thisclass, nest = 0):
  if nest > 1:
    print("    |" * (nest - 1), end = '')
  if nest > 0:
    print("    +---", end = '')
  print(thisclass.__name__)
  for subclass in thisclass.__subclasses__():
    PrintExcTree(subclass, nest + 1)

PrintExcTree(BaseException)
```

My `platform.python_version()` is `'3.5.3'` and this is what the tree looks like:

```
BaseException 
    +---Exception
    |    +---TypeError
    |    +---StopAsyncIteration
    |    +---ArithmeticError
    |    |    +---FloatingPointError
    |    |    +---OverflowError
    |    |    +---ZeroDivisionError
    |    +---EOFError
    |    +---SyntaxError
    |    |    +---IndentationError
    |    |    |    +---TabError
    |    +---ValueError
    |    |    +---UnicodeError
    |    |    |    +---UnicodeEncodeError
    |    |    |    +---UnicodeDecodeError
    |    |    |    +---UnicodeTranslateError
    |    |    +---UnsupportedOperation
    |    +---LookupError
    |    |    +---IndexError
    |    |    +---KeyError
    |    |    +---CodecRegistryError
    |    +---AttributeError
    |    +---BufferError
    |    +---error 
    |    +---MemoryError
    |    +---SystemError
    |    |    +---CodecRegistryError
    |    +---Warning
    |    |    +---UserWarning
    |    |    +---DeprecationWarning
    |    |    +---SyntaxWarning
    |    |    +---ImportWarning
    |    |    +---ResourceWarning
    |    |    +---FutureWarning
    |    |    +---BytesWarning
    |    |    +---RuntimeWarning
    |    |    +---PendingDeprecationWarning
    |    |    +---UnicodeWarning
    |    +---NameError
    |    |    +---UnboundLocalError
    |    +---AssertionError
    |    +---OSError
    |    |    +---ConnectionError
    |    |    |    +---BrokenPipeError
    |    |    |    +---ConnectionAbortedError
    |    |    |    +---ConnectionRefusedError
    |    |    |    +---ConnectionResetError
    |    |    +---BlockingIOError
    |    |    +---FileNotFoundError
    |    |    +---ChildProcessError 
    |    |    +---ItimerError
    |    |    +---NotADirectoryError
    |    |    +---ProcessLookupError
    |    |    +---PermissionError
    |    |    +---FileExistsError
    |    |    +---UnsupportedOperation
    |    |    +---TimeoutError
    |    |    +---IsADirectoryError
    |    |    +---InterruptedError
    |    +---ReferenceError
    |    +---ImportError
    |    |    +---ZipImportError
    |    +---StopIteration
    |    +---RuntimeError
    |    |    +---RecursionError
    |    |    +---NotImplementedError
    |    |    +---_DeadlockError
    |    +---Error
    +---GeneratorExit
    +---KeyboardInterrupt
    +---SystemExit
```
&mdash; Oliver Frolovs, 2020