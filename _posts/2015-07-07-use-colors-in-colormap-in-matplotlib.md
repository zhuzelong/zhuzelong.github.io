---
layout: post
title: Use colors in Colormap in Matplotlib
categories: [Record]
tags: [viz]
published: True

---
## Question

It is trivial to assign colors to Lines in matplotlib by specifying "named colors", e.g. `b` (blue), `k` (black). matplotlib provides various Colormaps for various situations. But how could one assign colors in a colormap to patches?

An [example](http://stanford.edu/~mwaskom/software/seaborn/generated/seaborn.kdeplot.html#seaborn.kdeplot) from *seaborn* tutorial:

```python
import seaborn as sns
import numpy as np

np.random.seed(10)

mean, cov = [0, 2], [(1, .5), (.5, 1)]
x, y = np.random.multivariate_normal(mean, cov, size=50).T

ax = sns.kdeplot(x, y, n_levels=30, cmap="Purples_d")
```

A bivariate KDE plot colored by the `Purples_d` colormap is rendered. But how about univariate KDE plot, which is more common?

```python
# The same setting as above
# -------------------------

ax = sns.kdeplot(x, cmap='Purples_d')
```

A `TypeError` is raised: `Line has no property cmap`. 

Moreover, I want to plot several KDE lines in one Axes to compare the distribution among groups and I need to use colors to differentiate groups. What should I do?


## Solution

Owing to the [post](http://stackoverflow.com/questions/8389636/creating-over-20-unique-legend-colors-using-matplotlib/8391452#8391452) in StackOverflow, a concise approach was provided. Assume that I have 5 groups and one variable to be estimated the kernel density.

```python
import matplotlib.pyplot as plt
import numpy as np

num_groups = 5

# Get a specific Colormap
cm = plt.get_cmap('Accent')

fig, ax = plt.subplots(1, 1)

# Set the color cycle
ax.set_color_cycle([cm(i / num_groups) for i in range(num_groups)])

# Plot KDE or CDF as usual
```

The key part is `ax.set_color_cycle`, which assign RGBA colors to patches in order and in cycle. `cm(i/num_groups)` returns a RGBA tuple. For example, `cm(0.2)` returns `(0.84392157793045053, 0.71058825254440305, 0.70901962518692008, 1.0)`.

Note that the arguments of `cm()` should be within `[0, 1]` and `i/num_groups` would return a float instead of 0 in Python 3. `cm` is an instance of `matplotlib.colors.LinearSegmentedColormap`.


## Colormap and scatter plot

*2015/7/19 update*

The following code did not work, all scatter points were in the same color and the `cmap` was not accessed.

```python
ax.set_color_cycle([cm(i/len(groups)) for i in range(len(groups))])

for name, group in gorups:
    ax.scatter(group['X'], group['Y'], label=name)
```

Referring to [the post](https://github.com/matplotlib/matplotlib/issues/3041), the devs of matplotlib believe that scatter plot is a special type of plot therefore does not need the color cycle. In other words, `ax.plot(x, y, '.')` and `ax.scatter(x, y)` are in fact different, although they would look identical in usual case.

Accordingly, it would be better to use `ax.plot(x, y, '.')` together with color map in my situation. Alternatively, use `ax.scatter(x, y, c=cm(name/len(groups)))`.



## Future work

It remains to probe the reason why 1D Line does not support `cmap` attribute while 2D Line does.

