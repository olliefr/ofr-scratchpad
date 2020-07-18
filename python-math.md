# Three little gems from Python `math` module

When programming in a multitude of languages with an aim to get the job done, small details are often missed. It's a trade-off. Today, while preparing for a Python certification exam, I have discovered, that Python's standard library `math` module has three incredibly useful functions which, in my experience, people (yours truly as well) tend to write themselves.

* `math.degrees(x)` converts angle *x* from radians to degrees.
* `math.radians(x)` converts angle *x* from degrees to radians.
* `math.hypot(*coordinates)` returns the Euclidean norm, `sqrt(sum(x**2 for x in coordinates))`. This is the length of the vector from the origin to the point given by the coordinates.

## More information

See [Python `math` module documentation](https://docs.python.org/3/library/math.html).
