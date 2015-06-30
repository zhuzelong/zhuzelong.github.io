---
layout: post 
title: Remarks on update of seaborn 0.6.0
categories: [Remarks]
tags: [viz]
published: True

---
Seaborn 0.6.0 is released today. Surprisingly, quite a few changes took place.

## Objective

As stated in the index page:

> Seaborn should be thought of as a complement to matplotlib, not a replacement for it. 

As I said in the last post, seaborn looks like an enhancement of matplotlib instead of a standalone distribution. As a result, I suppose users would have to play with matplotlib even using seaborn.

Moreover, the analogy with ggplot2 was deleted. I guess the author would not like to emulate ggplot2. So I am really looking forward to the ggplot in Python (developed by yhat).


## API

A number of API's are modified. More attention is paid to categorical data and API's are unified. It looks promising from the perspective of complement to matplotlib.

The author did not keep the old documentation, which from my point of view is quite radical. Although I do not have any "legacy" code but it might be better to render users with choice, as matplotlib does.

Overall, seaborn is nice if I treat it as another interface to matplotlib instead of an alternative to ggplot2. I think that `yhat/ggplot` is promising.
