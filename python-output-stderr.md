# Output to `stderr` in Python

*Yet another* way to output to the standard error stream in Python:

```Python
import sys

print("...", file = sys.stderr)
```

&mdash; Oliver Frolovs, 2020