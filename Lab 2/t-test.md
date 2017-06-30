CMTH642 - Exploring T-distribution
================

``` r
library(knitr)
```

    ## Warning: package 'knitr' was built under R version 3.3.3

``` r
opts_knit$set(upload.fun = function(file) imgur_upload(file, key = "00ec676f881f591"))
```

#### T-Distribution

``` r
# Generate some numbers
x <- seq(from =-5, to = 5, by=.1)

# Plot the probability distribution
plot(x, dt(x, df = 30), ylab='Probability',xlab='x', main="PDF of T-Distribution dt(x, df)")
```

![](http://i.imgur.com/qP1iJOJ.png)

``` r
# Generate another set of numbers
t.value <- seq(from = -3, to = 3, by=.1)

# Plot the cumulative distribution
plot(t.value, pt(t.value, df = 74), ylab='Cumulative Probability',xlab='T-Value', main="T-Distribution (CDF) pt(tvalues, df)")
```

![](http://i.imgur.com/soR64Db.png)

#### Calculations

``` r
# probability of getting a number smaller than (or equal to) the argument of pt function
# area under the curve from x to y 
pt(1, df=70) - pt(-1, df=70)
```

    ## [1] 0.6792451

``` r
pt(2, df=70) - pt(-2, df=70)
```

    ## [1] 0.9506184

``` r
pt(3, df=70) - pt(-3, df=70)
```

    ## [1] 0.9962623

``` r
# qt() returns the t-value at a given quantile
# qt(.95,30) --> 1.697261 means that 95% of of all numbers in the distribution are less than 1.69
# pt(1.69,30) --> ~ .95

# Generate some numbers
quantiles <- seq(from = 0.001 , to = .999, by=.001)

# Plot them
plot(qt(quantiles, df = 30), quantiles, xlab='Statistic(T-Value)',ylab='Quantile', main="T-Density Distribution (Inverse CDF) qt(quantiles, df)")
```

![](http://i.imgur.com/yPJTApo.png)

``` r
# notice symmetry
qt(c(.025, .975), df=30) # 30 degrees of freedom
```

    ## [1] -2.042272  2.042272
