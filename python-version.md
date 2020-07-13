# What Python version is that?!

* Check the Python version on the command line: `--version`, `-V`, `-VV`
* Check the Python version in a script: using `sys` and `platform`
  * The version *string* displayed at start: `sys.version`
  * A *named tuple* of version number components: `sys.version_info`
  * A *function* returning a *string*: `platform.python_version()`
  * A *tuple* of version number components: `platform.python_version_tuple()`

## Defensive coding

To ensure a script runs with a minimal version requirement of the Python interpreter one can use an assertion. More levels (micro, releaselevel, etc) can be added to the tuple, if necessary.

```Python
assert sys.version_info >= (2, 5)
```

## Examples

* The installed Python version can be determined from the **command line** using `--version`, `-V`, and `-VV` parameters.

    ```Shell
    $ python --version
    ```

    ```
    Python 3.7.8
    ```

    Or

    ```Shell
    $ python -V
    ```

    ```
    Python 3.7.8
    ```

    Or

    ```Shell
    $ python -VV
    ```

    ```
    Python 3.7.8 (tags/v3.7.8:4b47a5b6ba, Jun 28 2020, 08:53:46) [MSC v.1916 64 bit (AMD64)]
    ```

* To get the version number **from a script**, `sys` and `platform` modules are useful.
  
  * The *string* displayed when the interactive interpreter is started is `sys.version`
    
    ```Python
    import sys
    print(sys.version)
    ```
    
    ```
    3.7.8 (tags/v3.7.8:4b47a5b6ba, Jun 28 2020, 08:53:46) [MSC v.1916 64 bit (AMD64)]
    ```
  * The version information is also available as a *named tuple* `sys.version_info`
    
    ```Python
    import sys
    print(sys.version_info)
    ```
    
    ```
    sys.version_info(major=3, minor=7, micro=8, releaselevel='final', serial=0)
    ```
    
  * There is also a *function* `platform.python_version()` returning the version *string*.
  
    ```Python
    import platform
    print(platform.python_version())
    ```
    
    ```
    3.7.8
    ```
    
  * The latter information is also available as *function* which returns a *tuple*.
    
    ```Python
    import platform
    print(platform.python_version_tuple())
    ```
    
    ```
    ('3', '7', '8') 
    ```

  * There is a wealth of other information related to the Python build available in `platform`.

&mdash; Oliver Frolovs, 2020