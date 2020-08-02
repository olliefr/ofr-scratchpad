# Profile memory usage in Python

## Individual objects

```
Python 3.8.2 (default, Jul 16 2020, 14:00:26)
[GCC 9.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
```

```Python
>>> import sys
>>> sys.getsizeof({})
64
>>> sys.getsizeof([])
56
>>> sys.getsizeof(set())
216
```

## A single function or method

Use [memory-profiler](https://pypi.org/project/memory-profiler/) package. The decorator `@profile` can be put around any function or method and running

```Shell
$ python -m memory_profiler myscript
```

would produce line-by-line memory usage data once the script exits.

## Entire application

Rather than having to profile an entire application, use [guppy3](https://zhuyifei1999.github.io/guppy3/). The workflow is along the folowing lines.

```Python
from guppy import hpy

h = hpy()

print(h.heap())
```

This will print a table of usage grouped by object type. Here's an example of an new Python interpreter session:

```
Partition of a set of 143382 objects. Total size = 15643117 bytes.
 Index  Count   %     Size   % Cumulative  % Kind (class / dict of class)
     0  36882  26  3454101  22   3454101  22 str
     1  25485  18  2339280  15   5793381  37 tuple
     2   8460   6  1494124  10   7287505  47 types.CodeType
     3   1412   1  1318456   8   8605961  55 type
     4  17048  12  1273626   8   9879587  63 bytes
     5   8172   6  1111392   7  10990979  70 function
     6  26047  18   735680   5  11726659  75 int
     7   1412   1   700864   4  12427523  79 dict of type
     8    407   0   679320   4  13106843  84 dict of module
     9   1211   1   534256   3  13641099  87 dict (no owner)
<337 more rows. Type e.g. '_.more' to view.>
```

This type of profiling can be difficult in large applications using a relatively small number of object types.

## mprof

`mprof` (comes with the [memory-profiler](https://pypi.org/project/memory-profiler/) module) can show memory usage as a function of time (not line-by-line) over the lifetime of the application. This can be useful for verifying that memory is getting cleaned up and released periodically. To run it:

```Shell
$ mprof run script script_args
```

`mprof` will automatically create a graph of the script’s memory usage over time, which can be viewed by running `mprof plot`. 

Note that plotting requires `matplotlib`. 

&mdash; Oliver Frolovs, 2020