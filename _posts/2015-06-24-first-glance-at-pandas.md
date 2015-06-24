---
layout: default 
title: First glance at pandas
categories: []
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


## A confusing quick start

The quick start ("10 minute for pandas") is one of the worst quick start I have ever read. It takes a dozen of pages and explains nothing in detail. The examples are not representative but no more than excerpts of cookbook.

Besides, there is a chapter of cookbook and dozens of chapters of specific subjects. What are the difference among them? Which part should I refer to? The "Tutorial" part does not specify the objectives.

