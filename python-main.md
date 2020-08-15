# Where is `main()` function in a Python script?

* The following pattern protects the code from being run when a file containing it is `import`-ed. 
* The global variable `__name__` is set to `"__main__"` only when the script is run rather than being imported.
* Don't make `main()` fiddle with `sys.exit()`. Instead, make `main()` return the exit code &mdash; success (0) or failure (>0).

```Python
import sys

def main():
  return 0
  
if __name__ == "__main__":
  sys.exit(main())
```

&mdash; Oliver Frolovs, 2020