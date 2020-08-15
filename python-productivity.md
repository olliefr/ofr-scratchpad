# Setting up a productive Python environment

:::{tags}
Python IPython Pip Venv
:::

I work with Python 3.8 at the very least, so the _virtual environment_ is based on `venv`, which is the recommended approach for modern Python.

The recommendations in this note are universally useful and applicable regardless of the project's specifics.

## A better interpreter interface

Install `ipython` using `pip`:

```Shell
$ pip3 install ipython
```

Now `ipython` command is available and should be used for interactive work instead of standard `python` interpreter CLI.

## Why set up virtual environments?

The Python package manager `pip` by default installs (and updates) packages globally. This is not optimal since different programs may rely on different versions of the same package.

Furthermore, different versions of the *Python intepreter itself* might be required for different projects.

To resolve this, Python includes powerful tools to *manage dependencies* of our programs by creating *virtual environments*. 

The _virtual environment configuration_ file would store what Python interpreter version is used, as well as all PyPI modules utilised in the project and their version numbers.

## Setting up the virtual environment

This is done on per project basis. To create the environment:


* Create a project directory
* Change into the project directory
* Run `python3 -m venv <name_of_virtualenv>`

Example of the last step:

```Shell
project-folder$ python3 -m venv env
```

Now can activate the environment:

```Shell
project-folder$ source env/bin/activate
```

The shell prompt gets replaced by the environment's shell prompt:

```Shell
(env) $
```


Note, that the directories and files comprising the *virtual environment* itself are automatically added to the `.gitignore` file and will not be (and should not be) checked into the revision control system.

In other words, only the *virtual environment* configuration will be stored in the revision control system, and when necessary, the *virtual environment* will be recreated by the Python tools.

## Using the virtual environment

Now when `pip` is invoked, it will install the packages into the current project's *environment* and all project's dependencies can be version controlled and managed.

For example, install the `requests` module into the current *environment* (project):

```Shell
(env) $ pip install requests
```

Remember what packages are installed so that this information can be stored under revision control and used for deployment as well:

```Shell
(env) $ pip freeze > requirements.txt
```

The `requirements.txt` appears to be a magic name `pip` and other Python tooling know about. It should be stored in the _revision control system_ and will be useful for deploying an application to _production_.

## Leaving the virtual environment

To leave the *virtual environment*, run `deactivate`:

```Shell
(env) $ deactivate
```

This will take you to the familiar `bash` prompt outside of the Python *virtual environment*.

## More information on the virtual environments

[RealPython's _What Virtual Environments Are Good For?_](https://realpython.com/lessons/what-virtual-environments-are-good-for/) and the materials linked from there.

&mdash;Oliver Frolovs, 2020