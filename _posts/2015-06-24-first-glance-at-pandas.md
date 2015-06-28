---
layout: post
title: First glance at pandas
categories: [Remarks]
tags: [pandas]
published: True

---
I have been working on a data mining project with R for two months and I felt comfortable with R. In spite of some weird naming rules in R, I found it intuitive and swift to implement exploratory data analysis in R, especially with the help of `data.table` and `ggplot2`.

`caret` is a comprehensive machine learning library but it seems to focus on supervised learning (classification and regression). By contrast, `scikit-learn` supports both supervised and unsupervised learning, plus metrics and evaluation. Therefore, I will turn to Python to carry out clustering.

Numpy is the dependency of various data mining packages in Python. However, the `ndarray` is more like an array where elements have to be of the same data type. It is quite convenient to apply algorithms to a tidy matrix in Python or Matlab, but the real world is often more complicated. This is the reason why I am in favour of R: the `data.frame` is more adaptive to the real world. Consequently, pandas is a counterpart of `data.frame` in Python. I read the manual of pandas, a 1680 page document and I soon became annoyed with it.

## Legacy API

The first thing confusing me is the API. I can index a data frame by `.loc`, `.iloc`, `.ix`, `.at`, `.iat`. Why do I need so many resembling API? StackOverflow told me that `.ix` is a legacy and should be obsolete.

By contrast, `data.table` provides a unified indexing API: `[`, and accessing to data is same as writing an SQL query, really intuitive.

## Naming rules

pandas tries to imitate `data.frame` so provides similar API's in `data.frame`. But the names looks weird.

1. Why does pandas use `.describe()` for `summary()` in R? To show pandas is different?
2. When you want to read an external csv file (similar to other file types), it sounds reasonable to invoke `read_csv()`. But when would I use `to_csv()` when I want to write a data frame to a csv file? Why not `write_csv()`? Another distinction from R?

There are a lot more counter-intuitive names in pandas. It does not have to be in this way to distinguish itself from R.


## Duplicate API

A quick example: what is the difference between `.concatenate()` and `append()`? As far as I searched the answer on SO, they seems duplicate. 

In `data.table`, the columns are bound as local variable in a data table thus columns can be accesses without binding the name of data table. For example,

```R
# Return two columns of a data table 'dt'
dt[, list(col_1, col_2)]
```

In pandas, a simple "if-then" accessing looks like:

```Python
df.loc[df.col_1 > 0, 'col_2']
```

As you can see, two distinct ways are entailed to access a column on condition: `df.col_1` and `'col_2'`. Why do I have to remember whether to use a quote? Such inconsistency is annoying.


## Summary

One of the philosophy of Python is that "there is only one best choice". pandas, as an ambitious library, seems to violate the rule. Moreover, it emulates `data.frame` in R, but is far from "good" compared with `data.table`. Why not keep it simple, concise and consistent?