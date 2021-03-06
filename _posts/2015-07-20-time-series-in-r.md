---
layout: post
title: Time Series in R
categories: [Record]
tags: [time series]
published: True

---
## Prologue

I have been working on time series analysis for two weeks. At the beginning, I worked in Python and I soon found it incompetent of dealing with time series. The `ARIMA` model in `statsmodels` package is premature. I then switched to R, which has a mature built-in functions and data structure for time series analysis.

I became confused about the `ts` in R. It took me almost a week to understand the `ts`.


## Questions

### Q1. date and ts
Python has a complete set of objects to store date and time: `datetime.date`, `datetime.time`. R has `Date`, `POSIXct` and `POSIXlt`. Why do we need another time data `ts`?


### Q2. what is the season/unit time of `ts`?

I read quite a few tutorials about `ts` and most of them begin with:

```r
t = ts(x, start=2010, freq=12)
```

then you would have a monthly time series. So you would probably think: *2010 indicates the year, and there are 12 months in a year*. But what if you have a daily data or even hourly data? Some may told you to use `freq=365.25` and `freq=365.25*24` respectively. However, what does this all mean? If you have a **frequency**, then where is the **season**?


## My Answers

### Date and ts are different

It is intuitive to distinguish `Date` (not restricted to R) and `ts`. The former is a single point in time and the latter is a flow of time. Date and time are used as the indices ot `ts`, or not (you would see it in the next section).


### Look inside `ts`

As the documentation of the function `ts()` shows:

> frequency: the number of observations per unit of time.

So what is the "unit of time" (aka. "season"). The answer is: just a "unit" of time. It is not a "year", a "month" or a "week". In other words, **you cannot define the "metric" of season, and R does not care the "metric" of season either**.

Let's look back at the example of most of the tutorials. You might think `2010` indicates year 2010, but in fact it is just a **number**. See the following example:

```r
> t = ts(1:24, start=2010, frequency=12)
> t
     Jan Feb Mar Apr May Jun Jul Aug Sep Oct Nov Dec
2010   1   2   3   4   5   6   7   8   9  10  11  12
2011  13  14  15  16  17  18  19  20  21  22  23  24

> t = ts(1:24, start=-1, frequency=12)
> t
   Jan Feb Mar Apr May Jun Jul Aug Sep Oct Nov Dec
-1   1   2   3   4   5   6   7   8   9  10  11  12
0   13  14  15  16  17  18  19  20  21  22  23  24

> t = ts(1:24, start=2010, frequency=4)
> t
     Qtr1 Qtr2 Qtr3 Qtr4
2010    1    2    3    4
2011    5    6    7    8
2012    9   10   11   12
2013   13   14   15   16
2014   17   18   19   20
2015   21   22   23   24
```

R showed months and quarters, it seems that R does understand the meaning of `2010` and interpret months and quarters correctly, doesn't it? More example.

```r
> t = ts(1:54, start=2012, frequency=52)
> t
Time Series:
Start = c(2012, 1) 
End = c(2013, 2) 
Frequency = 52 
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20
[21] 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40
[41] 41 42 43 44 45 46 47 48 49 50 51 52 53 54
```

There 53 weeks in 2012 (a leap year) but the last two values were considered as the first two weeks in `2013` since the `frequency` is 52.

In order to have a closer look at how R treats the date and time of `ts`:

```r
> t = ts(1:54, start=2012, frequency=52)
> index(t)
[1] 2012.000 2012.019 2012.038 2012.058 2012.077 2012.096
 [7] 2012.115 2012.135 2012.154 2012.173 2012.192 2012.212
[13] 2012.231 2012.250 2012.269 2012.288 2012.308 2012.327
[19] 2012.346 2012.365 2012.385 2012.404 2012.423 2012.442
[25] 2012.462 2012.481 2012.500 2012.519 2012.538 2012.558
[31] 2012.577 2012.596 2012.615 2012.635 2012.654 2012.673
[37] 2012.692 2012.712 2012.731 2012.750 2012.769 2012.788
[43] 2012.808 2012.827 2012.846 2012.865 2012.885 2012.904
[49] 2012.923 2012.942 2012.962 2012.981 2013.000 2013.019
```

Moreover, the second argument of `start` is not the month or quarter, it is the index of the observation in one season.

```r
> t = ts(1:24, start=c(100, 3), frequency=8)
> t
Time Series:
Start = c(100, 3) 
End = c(103, 2) 
Frequency = 8 
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20
[21] 21 22 23 24
```

The first 6 observations is in the season "100", then 8 observations in the season "101", another 8 in "102" then last 2 in "103".


A short conclusion: the season in `ts` is just a number and the date (or datetime) in `ts` is also a number (float). You would probably get confused and struggle to store a daily time series if you think the season is "year".


### Daily data in `ts`
Given the examples, you might think that the unit of time in `ts` is "year" and it is difficult to store daily data due to the leap year (`freq=365` or `freq=365.25`?). Remember the short conclusion: the **unit** of time is no more than a unit, it is not "year" or "day".

```r
library(zoo)

# Make dates
> idx = seq(as.Date('2015-1-1'), as.Date('2015-1-24'), by='day')
# Make a zoo
> z = zoo(1:24, idx)
> z
2015-01-01 2015-01-02 2015-01-03 2015-01-04 2015-01-05 2015-01-06 
         1          2          3          4          5          6 
2015-01-07 2015-01-08 2015-01-09 2015-01-10 2015-01-11 2015-01-12 
         7          8          9         10         11         12 
2015-01-13 2015-01-14 2015-01-15 2015-01-16 2015-01-17 2015-01-18 
        13         14         15         16         17         18 
2015-01-19 2015-01-20 2015-01-21 2015-01-22 2015-01-23 2015-01-24 
        19         20         21         22         23         24

# Convert zoo to ts
> t = as.ts(z)
> t
Time Series:
Start = 16436 
End = 16459 
Frequency = 1 
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20
[21] 21 22 23 24
```

The `Frequency` ot `t` is 1. Does it indicate one observation per year (if you think the unit of time is "year")? Have a look at the `Start` and `End`.

```r
> as.Date(16436)
[1] "2015-01-01"
> as.Date(16459)
[1] "2015-01-24"
```

It is apparent that the time series `t` is daily-based and `Frequency=1` means one observation per **day**. The number is the elapsed days since `1970-01-01` (day 0).



## One more thing

`ts` in R can only deal with strictly regular time series, i.e. no interruption in the time series. Use `zoo` to store non-strictly regular time series and convert it to `ts`. R would fill `NA` in the time series, which is necessary in decomposition and ARIMA analysis.

### `ts()` or `as.ts()`?

There is no additional argument in `as.ts` thus the frequency of `as.ts()` is always 1. If you need to decompose the time series with `decompose(t)` then it would fail because `decompose()` is only applicable to seasonal data of which `frequency` is larger or equal to 2. Therefore, you would need to convert a `zoo` to `ts` by `ts(z, start=, frequency=)` and be careful with `start`. The resulting time series of `ts(z)` is continuous thus it would ignore the dates in the original `zoo`. Be careful when the time series is not strictly regular, no `NA` will be interpolated, which incurs an alignment problem.

In ARIMA analysis, it is sufficient to use `arima(z, ...)` since the `z` would be implicitly converted to `ts` by `as.ts(z)`. If `z` is not strictly regular, then `NA` would by interpolated in the new `ts` in order to align the dates with dates in `z`. `arima` is able to deal with `NA` so do not convert manually by invoking `ts(z, start=, frequency=)` or bother with the start date and frequency.


