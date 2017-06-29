CMTH 642 - Lab 2
================

#### Question 1

We want to test with 95 percent confidence interval whether the volume of a shipment of lumber is as usual (mu=39000 cubic feet). Use data&lt;-rnorm(n, mean = , sd = ) to generate 75 shipments with mean:36500 and sd:2000. Use set.seed(0) before rnorm to regenerate the same data if required. On the simulated data test Ho: mu = 39000

(Hint: t.test(data, mu = 39000))

``` r
set.seed(0)
# Simulate 75 shipments
lumber_data <- rnorm(n=75, mean=36500, sd=2000)

# Perform two-sided(default) t-test on lumber_data
t.test(lumber_data, mu=39000, conf.level=0.95)
```

    ## 
    ##  One Sample t-test
    ## 
    ## data:  lumber_data
    ## t = -12.288, df = 74, p-value < 2.2e-16
    ## alternative hypothesis: true mean is not equal to 39000
    ## 95 percent confidence interval:
    ##  36033.60 36861.38
    ## sample estimates:
    ## mean of x 
    ##  36447.49

``` r
# Since the returned p-value is less than the significance level of 0.05, we can reject the null hypothesis. There is significant evidence that the mean volume of lumber shipment is different from the usual level of 39000 cubic feet.
```

#### Question 2

The results obtained for an intelligence test in 10 subjects are: 65, 78, 88, 55, 48, 95, 66, 57, 79, 81

i- Calculate the sample mean and standard deviation

``` r
intel_results <- c(65, 78, 88, 55, 48, 95, 66, 57, 79, 81)
paste0("Sample mean is: ",mean(intel_results))
```

    ## [1] "Sample mean is: 71.2"

``` r
paste0("Sample standard deviation is: ",sd(intel_results))
```

    ## [1] "Sample standard deviation is: 15.3463712685153"

ii- Use a one-sample t-test to determine whether the average result of the population which received the same test is equal to 75 using a significance level of 0.05.

``` r
t.test(intel_results, mu=75, conf.level=0.95) 
```

    ## 
    ##  One Sample t-test
    ## 
    ## data:  intel_results
    ## t = -0.78303, df = 9, p-value = 0.4537
    ## alternative hypothesis: true mean is not equal to 75
    ## 95 percent confidence interval:
    ##  60.22187 82.17813
    ## sample estimates:
    ## mean of x 
    ##      71.2

``` r
# Since the returned p-value is greater than the significance level of 0.05, we cannot reject the null hypothesis. There is no evidence that the test results are significantly different from 75. 
```

#### Question 3

A bottle filling machine is set to fill bottles with soft drink to a volume of 500 ml. The actual volume is known to follow a normal distribution. The manufacturer believes the machine is under-filling bottles. A sample of 20 bottles is taken and the volume of liquid inside is measured.

The volumes were: 484.11, 459.49, 471.38, 512.01, 494.48, 528.63, 493.64, 485.03, 473.88, 501.59, 502.85, 538.08, 465.68, 495.03, 475.32, 529.41, 518.13, 464.32, 449.08, 489.27

i- Calculate the sample mean and standard deviation

``` r
bottle_data <- c(484.11, 459.49, 471.38, 512.01, 494.48, 528.63, 493.64, 485.03, 473.88, 501.59, 502.85, 538.08, 465.68, 495.03, 475.32, 529.41, 518.13, 464.32, 449.08, 489.27)

paste0("Sample mean is: ",mean(bottle_data))
```

    ## [1] "Sample mean is: 491.5705"

``` r
paste0("Sample standard deviation is: ",sd(bottle_data))
```

    ## [1] "Sample standard deviation is: 24.7936843560486"

ii- Use a one-sample t-test to determine whether the bottles are being consistently under filled using a significance level of 0.01.

``` r
t.test(bottle_data, mu=500, alternative="less", conf.level=0.99)
```

    ## 
    ##  One Sample t-test
    ## 
    ## data:  bottle_data
    ## t = -1.5205, df = 19, p-value = 0.07243
    ## alternative hypothesis: true mean is less than 500
    ## 99 percent confidence interval:
    ##      -Inf 505.6495
    ## sample estimates:
    ## mean of x 
    ##  491.5705

``` r
# Since the returned p-value is greater than the significance level of 0.01, we cannot reject the null hypothesis. There is no evidence that the bottles are being under-filled.
```

#### Question 4

An outbreak of Salmonella-related illness was attributed to ice cream produced at a certain factory. Scientists measured the level of Salmonella in 9 randomly sampled batches of ice cream.

The levels (in MPN/g) were: 0.593 0.142 0.329 0.691 0.231 0.7930.5190.392 0.418

Is there evidence that the mean level of Salmonella in the ice cream is greater than 0.3 MPN/g?

``` r
icecream_data <- c(0.593, 0.142, 0.329, 0.691, 0.231, 0.793, 0.519, 0.392, 0.418)
t.test(icecream_data, mu=0.3, alternative="greater", conf.level = 0.95)
```

    ## 
    ##  One Sample t-test
    ## 
    ## data:  icecream_data
    ## t = 2.2051, df = 8, p-value = 0.02927
    ## alternative hypothesis: true mean is greater than 0.3
    ## 95 percent confidence interval:
    ##  0.3245133       Inf
    ## sample estimates:
    ## mean of x 
    ## 0.4564444

``` r
# Since the returned p-value is less than the significance level of 0.05, we can reject the null hypothesis. There is significant evidence that the mean level of Salmonella in the ice cream is gerater than 0.3 MPN/g.
```

#### Question 5

Assuming that the data in mtcars follows the normal distribution, find the 95% confidence interval estimate of the difference between the mean gas mileage of manual and automatic transmissions.

(Hint: two sample t-test)

``` r
manual_cars <- mtcars$mpg[mtcars$am == 1]
auto_cars <- mtcars$mpg[mtcars$am == 0]

t.test(manual_cars, auto_cars, mu=0, conf.level=0.95)
```

    ## 
    ##  Welch Two Sample t-test
    ## 
    ## data:  manual_cars and auto_cars
    ## t = 3.7671, df = 18.332, p-value = 0.001374
    ## alternative hypothesis: true difference in means is not equal to 0
    ## 95 percent confidence interval:
    ##   3.209684 11.280194
    ## sample estimates:
    ## mean of x mean of y 
    ##  24.39231  17.14737

``` r
# Since the returned p-value is less than the significance level of 0.05, we can reject the null hypothesis. There is significant evidence that the mean gas mileages between manual and automatic transmission are diferent. 
```

#### Question 6

Consider the gain in weight of 19 female rats between 28 and 84 days after birth. 12 were fed on a high protein diet and 7 on a low protein diet. Using the following data, test the hypothesis that there is no difference in weight gain between female rats raised on a high-protein diet versus those raised on a low-protein diet. Use a significance level of 0.05 and assume equal variances. ("Hint: var.equal=TRUE")

High protein: 134,146,104,119,124,161,107,83,113,129,97,12 Low protein: 70,118,101,85,107,132,94

``` r
high_protein <- c(134,146,104,119,124,161,107,83,113,129,97,12)
low_protein <- c(70,118,101,85,107,132,94)

t.test(high_protein, low_protein, mu=0, var.equal=TRUE, conf.level=0.95)
```

    ## 
    ##  Two Sample t-test
    ## 
    ## data:  high_protein and low_protein
    ## t = 0.62634, df = 17, p-value = 0.5394
    ## alternative hypothesis: true difference in means is not equal to 0
    ## 95 percent confidence interval:
    ##  -23.09271  42.59271
    ## sample estimates:
    ## mean of x mean of y 
    ##    110.75    101.00

``` r
# Since the returned p-value is greater than the significance level of 0.05, we cannot reject the null hypothesis. Ther is no evidence that the weight gains between female rats raised on high vs. low protein diet are different. 
```

#### Question 7

Load the "MASS" package. In the "immer" dataset of the "MASS" library, we have: Y1 Yield in 1931, Y2 Yield in 1932. Assuming that the data in "immer" follows the normal distribution, find the 95% confidence interval estimate of the difference between the mean barley yields between years 1931 and 1932 (Hint: paired t-test). Get "p.value" in a variable pvalue and "statistic" in a variable st.

(Hint: ttest&lt;-t.test(.,.,.) and then names(ttest))

``` r
# Load the MASS library and store barley yield data for 1931 and 1932
library(MASS)
yield_1931 <- immer$Y1
yield_1932 <- immer$Y2

# Run t.test between the yield data for the two years and store the results
barley_test <- t.test(yield_1931, yield_1932, mu=0, paired=TRUE, conf.level=0.95)

# Display the variables of the test results
names(barley_test)
```

    ## [1] "statistic"   "parameter"   "p.value"     "conf.int"    "estimate"   
    ## [6] "null.value"  "alternative" "method"      "data.name"

``` r
# Store the p.value and statistic variables
pvalue <- barley_test$p.value
st <- barley_test$statistic
```

#### Question 8

A professor takes a random sample of students enrolled in her course. She finds the following: in the sample, there are 25 freshmen, 32 sophomores, 18 juniors, and 20 seniors. Test the null hypothesis that freshman, sophomores, juniors, and seniors are equally represented among students signed up for this course.

(Hint: chi-square test)

``` r
students <- c("Freshmen"=25, "Sophomores"=32, "Juniors"=18, "Seniors"=20)
chisq.test(students)
```

    ## 
    ##  Chi-squared test for given probabilities
    ## 
    ## data:  students
    ## X-squared = 4.9158, df = 3, p-value = 0.1781

``` r
# At 95% confidence level, since the returned p-value is greater than the significance level of 0.05, we cannot reject the null hypothesis. There is no evidence that the groups of students are not equally represented. 
```
