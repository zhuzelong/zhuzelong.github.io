---
layout: post
title: Forsake Seaborn
categories: [Remarks]
tags: [viz]
published: True

---
After the enormous adjustment of API in *Seaborn*, I found it of little value to data analysis compared with *ggplot* or even *matplotlib*.

Today I tried to use `tsplot` in *Seaborn* but I soon found out that the `date` data cannot be used the `tsplot` (c.f. [here](http://stackoverflow.com/questions/22795348/plotting-time-series-data-with-seaborn/22798911#22798911)). Surprising! Why is it named `tsplot` while the data in X-axis has to be an integer or float?

It took me 2 minutes to accomplish the time series plot in R with ggplot. I just need to ensure the data in X-axis is `Date` and here came a **Time Series Plot**. When I tried to carry out time series analysis, I want the X-axis to indicate a **time** or **date** and Y-axis the metric. It is not so difficult, isn't it? Although it usually take efforts to specify the datetime format and the date break.


**ggplot** by yhat could not deal with date by `scale_x_date()` either. What are these Pythoner thinking about?
