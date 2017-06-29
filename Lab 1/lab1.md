CMTH 642 - Lab 1
================

#### Question 1

Read the "train.csv" file from the following website. "<https://raw.githubusercontent.com/agconti/kaggle-titanic/master/data/train.csv>"

``` r
train_data <- read.csv(url("https://raw.githubusercontent.com/agconti/kaggle-titanic/master/data/train.csv"))
```

#### Question 2

Have a look at the data set.

``` r
str(train_data)
```

    ## 'data.frame':    891 obs. of  12 variables:
    ##  $ PassengerId: int  1 2 3 4 5 6 7 8 9 10 ...
    ##  $ Survived   : int  0 1 1 1 0 0 0 0 1 1 ...
    ##  $ Pclass     : int  3 1 3 1 3 3 1 3 3 2 ...
    ##  $ Name       : Factor w/ 891 levels "Abbing, Mr. Anthony",..: 109 191 358 277 16 559 520 629 417 581 ...
    ##  $ Sex        : Factor w/ 2 levels "female","male": 2 1 1 1 2 2 2 2 1 1 ...
    ##  $ Age        : num  22 38 26 35 35 NA 54 2 27 14 ...
    ##  $ SibSp      : int  1 1 0 1 0 0 0 3 0 1 ...
    ##  $ Parch      : int  0 0 0 0 0 0 0 1 2 0 ...
    ##  $ Ticket     : Factor w/ 681 levels "110152","110413",..: 524 597 670 50 473 276 86 396 345 133 ...
    ##  $ Fare       : num  7.25 71.28 7.92 53.1 8.05 ...
    ##  $ Cabin      : Factor w/ 148 levels "","A10","A14",..: 1 83 1 57 1 1 131 1 1 1 ...
    ##  $ Embarked   : Factor w/ 4 levels "","C","Q","S": 4 2 4 4 4 3 4 4 4 2 ...

#### Question 3

Change the "Pclass" and "Survived" attributes to factors.

``` r
# create a vector with the two attribute names
names <- c('Pclass', 'Survived')

# convert the two attributes to factors and show summary of dataset to verify
train_data[,names] <- lapply(train_data[,names], factor)
str(train_data)
```

    ## 'data.frame':    891 obs. of  12 variables:
    ##  $ PassengerId: int  1 2 3 4 5 6 7 8 9 10 ...
    ##  $ Survived   : Factor w/ 2 levels "0","1": 1 2 2 2 1 1 1 1 2 2 ...
    ##  $ Pclass     : Factor w/ 3 levels "1","2","3": 3 1 3 1 3 3 1 3 3 2 ...
    ##  $ Name       : Factor w/ 891 levels "Abbing, Mr. Anthony",..: 109 191 358 277 16 559 520 629 417 581 ...
    ##  $ Sex        : Factor w/ 2 levels "female","male": 2 1 1 1 2 2 2 2 1 1 ...
    ##  $ Age        : num  22 38 26 35 35 NA 54 2 27 14 ...
    ##  $ SibSp      : int  1 1 0 1 0 0 0 3 0 1 ...
    ##  $ Parch      : int  0 0 0 0 0 0 0 1 2 0 ...
    ##  $ Ticket     : Factor w/ 681 levels "110152","110413",..: 524 597 670 50 473 276 86 396 345 133 ...
    ##  $ Fare       : num  7.25 71.28 7.92 53.1 8.05 ...
    ##  $ Cabin      : Factor w/ 148 levels "","A10","A14",..: 1 83 1 57 1 1 131 1 1 1 ...
    ##  $ Embarked   : Factor w/ 4 levels "","C","Q","S": 4 2 4 4 4 3 4 4 4 2 ...

#### Question 4

Check the missing values of the "Age" and "Name" attributes.

``` r
# sum any NAs for each column
colSums(is.na(train_data))
```

    ## PassengerId    Survived      Pclass        Name         Sex         Age 
    ##           0           0           0           0           0         177 
    ##       SibSp       Parch      Ticket        Fare       Cabin    Embarked 
    ##           0           0           0           0           0           0

#### Question 5

For a title containing a missing value, assign the mean age value for each title not containing a missing value.

(Hint: grepl(" Mr.\\.", train.data$Name))

``` r
# create list of titles
titles <- list("Mr", "Mrs", "Dr", "Miss", "Master")

# loop to calculate mean age for each title and assign that value to missing ages
for (title in titles){
  mean.title <- mean(train_data$Age[grepl(paste0(" ",title,"."), train_data$Name) & !is.na(train_data$Age)])
  train_data$Age[grepl(paste0(" ",title,"."),train_data$Name) & is.na(train_data$Age)]= mean.title
}
```

#### Question 6

List the distribution of Port of Embarkation. Replace empty entries with NA for "Embarked" attribute.

``` r
# description of attribute
str(train_data$Embarked)
```

    ##  Factor w/ 4 levels "","C","Q","S": 4 2 4 4 4 3 4 4 4 2 ...

``` r
# display tabular results for the attribute
table(train_data$Embarked, useNA = "ifany")
```

    ## 
    ##       C   Q   S 
    ##   2 168  77 644

``` r
# replace empty entries with NA
train_data$Embarked<-replace(train_data$Embarked,train_data$Embarked == "", NA)

# review tabular results
table(train_data$Embarked, useNA = "ifany")
```

    ## 
    ##         C    Q    S <NA> 
    ##    0  168   77  644    2

``` r
# count NAs in the attribute
sum(is.na(train_data$Embarked))
```

    ## [1] 2

#### Question 7

Assign the two missing values to the most counted port, which is Southampton in this case.

``` r
# assign 'S' for NAs
train_data$Embarked[which(is.na(train_data$Embarked))] = 'S'

# review tabular results to verify that NAs have been modified 
table(train_data$Embarked, useNA = "ifany")
```

    ## 
    ##       C   Q   S 
    ##   0 168  77 646
