# Storing configuration in a class

:::{tags}
\#python
:::

I've just seen this technique in a video. I haven't decided whether I like it or not yet. It is about storing program configuration *in a Python class*:

```Python
class config:
  """Global Configuration"""
  factor = 7.3
  threshold = 12
```

And the class variables can be accessed in the following way:

```Python
if num > config.threshold:
  num /= config.factor

```

Hmm&mldr;

&mdash;Oliver Frolovs, 2020