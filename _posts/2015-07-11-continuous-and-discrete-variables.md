---
layout: post
title: Continuous and discrete variables
categories: [Record]
tags: [viz]
published: True

---
## Continuous and discrete variables

Continuous and discrete variables are in the "lesson one" in statistics. However, I forgot such an elementary lesson when I worked on data analysis project.

According to the definitions:

> Continuous variables are those can take **any** and **infinite** values between an interval (including `[-inf, +inf]`).

and 

> Discrete variables are those only take **finite** number of values.


The definitions are intuitive to understand but things get complicated in reality. It is the complication that would probably make practitioners forget about the basis. Think about the following examples and find out if they are continuous or discrete variables.

1. weights of a human being
2. the number of planets in the universe
3. the number of human being that have been born since the very beginning
4. the winning time of a 100M athlete winning the game
5. the rounded winning time of a 100M athlete winning the game
6. the number of clients inflow (one of the questions in my project)


## Why is it important

It is often easy to make a bunch of plots in modern analysis tools, e.g. matplotlib, ggplot2. A set of beautiful graphs are usually at hand such as KDE plot, CDF plot, heatmap, boxplot, time series plot. But the key question is: what type of plot should we use in visualize a/several variable(s)?

For example, I used KDE plot to show the distribution of the size of clients. It looks nice since the sample is large and KDE could be applied to such a big sample. Then I tried using KDE plot to show the size of another feature, whose values range in `(1, 2, 3)` and came across the problem. In fact, the two variable I worked on are discrete thus I should not use KDE which is applicable to continuous variables. The plots can be shown does not mean the plots are correct.


## Conclusion

Concerning the example in my project, I used empirical CDF plot to show the distributions. An increasing number of ready packages and tools are available to the practitioners but we should think twice before picking from the repository.

