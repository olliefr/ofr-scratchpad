# Structuring a Python application

This is also passionately known as the _boilerplate code_. This note was inspired by a [_Real Python_ tutorial](https://realpython.com/python-application-layouts/).

Common task&hairsp;&mdash;&hairsp;capture dependencies for both tests and code:

```Shell
$ pip install -r requirements.txt
```

`LICENSE` information: if no _license_ (file?) is included with the code, the code is _fully copyrighted by default_ in most jurisdictions. This means _no one_ has a right to use it or copy it in any fashion! I'm using **MIT License** for my Python templates.

## One-off script

This template is for a _single-file_ Python program, often called a _script_.

It works both for code with or without dependencies. To manage dependencies, create a [virtual environment].

To begin, _generate_ a new repository using [python-template-oneoff] _template repository_.

To **run the unit test suite** for the script:

```Shell
$ python -m unittest tests.py
```

[virtual environment]: https://docs.python.org/3/tutorial/venv.html
[python-template-oneoff]: https://github.com/olliefr/python-template-oneoff.git

## Installable single package

This template steps up in complexity. It is a _multi-file_ Python _module_.

* Now there are _multiple_ Python files, grouped into a _module_.
* Now there are _multiple_ test files. The _test coverage_ is checked as well.
* Another tool useful for larger programs is a _linter_ (`pyflake`, `pep8`).

To begin, _generate_ a new repository using [python-template-single-package] _template repository_.

To **run the tests**, there is a `runtests.sh` bash script:

* it runs the tests;
* it runs the _test coverage_ tool from PyPI [coverage] suite;
* it can be made to run a _linter_ at the end, as well.

[python-template-single-package]: https://github.com/olliefr/python-template-single-package.git
[coverage]: https://pypi.org/project/coverage/

## Flask

TODO this template is an example of a _multi-module_ Python program.

## Django

TODO
