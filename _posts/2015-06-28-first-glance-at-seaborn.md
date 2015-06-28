---
layout: 
title: First glance at seaborn
categories: [Remarks]
tags: [seaborn]
published: True

---
I begin to read the tutorial of seaborn as I am considering to use seaborn in my project. I turn to seaborn for the following reasons:

1. I heard that seaborn is similar to ggplot2 in R, which is a well structured plot framework.
2. seaborn in built on matplotlib, the "golden standard" of plot framework in Python world.
3. There is a ggplot imitator in Python developed by yhat, but it seems to be premature. But I am looking forward to it.


Not surprisingly, the tutorial of seaborn disappointed me as I am so fond of ggplot2. It is evident that seaborn does not plot by *layers*, but putting everything together, entails a bunch of parameters. There are so many parameters that the list of parameters in the "API reference" page is incomplete. When I read the examples in the tutorial, I kept asking "where the parameter come from and what it is for" as I could not find it in the API reference.

Another issue regarding the plots in seaborn is the data. I have read a few tutorials and chapters of books on plotting, most of them made up some samples with `random.randn` which follow a Gaussian distribution. As a result, the scatter plot, histogram, contour plot and density plot of such data would look nice. However, the data in my project is skew such that the common plots are difficult to read. The real world data does not usually follow a Gaussian distribution perfectly, so the practitioners have to spend effort to tweak the plots. The tutorials tend to "show off" what the packages are able to do by demonstrating a lot of plots, but neglect how to tweak the plots to visualize the data better.

Moreover, plots serve to "speak of data", not "show off the beauty". I saw a few mixed plots where various types of plots or components are put together. They look beautiful and seem to convey much information. However, can human being read the information from such plots? I suppose that Python practitioners are inclined to show "I can do all such things" while R practitioners are likely to show "I need to accomplish these tasks".

The third reason why I do not like seaborn so much is that it is not a complete encapsulation of matplotlib. As stated before, I turned to seaborn because I need a "quick" tool for visualization while I do not have much time to learn matplotlib during my project. seaborn is an enhancement of matplotlib, providing a few more nice interface. But I have to go back to matplotlib very **often**.

