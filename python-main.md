# A pattern for the main function in a Python script

Don't make `main()` fiddle with system exit, if it does not need to. Make it raise an exception or return a positive integer value on error, instead:

```Python
import sys

def main():
  pass
  
if __name__ == "__main__":
  sys.exit(main())
```

&mdash; Oliver Frolovs, 2020