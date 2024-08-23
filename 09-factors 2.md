# Factors {#factors}


* **Factors** in **R** were created to represent **categorical variables** in statistics.

* **Categorical Variable:**
    + **Categorical variables** represent membership in some category rather than a numerical value **(e.g., blood type, country, language spoken, treatment group)**.
    
    + **Categorical variables** can only assume one of a finite collection values.
    
    + It does not usually make sense to make **numerical comparisons** between categorical variables.

## Definition of Factors

* In **R**, a factor can be thought of as a vector that
contains **specific extra information** about that vector.
    + More specifically, a factor is a vector that has certain **attributes** that
    distinguish from non-factor vectors.

* One key attribute stored by a factor vector is its **levels**. 

* The **levels** of a factor vector determine the **set of allowable values** in that vector.

* For example, let's look at the **group** variable in the **PlantGrowth** dataset 

```r
data(PlantGrowth)
PlantGrowth$group
```

```
##  [1] ctrl ctrl ctrl ctrl ctrl ctrl ctrl ctrl ctrl ctrl trt1 trt1 trt1 trt1 trt1
## [16] trt1 trt1 trt1 trt1 trt1 trt2 trt2 trt2 trt2 trt2 trt2 trt2 trt2 trt2 trt2
## Levels: ctrl trt1 trt2
```

* The **group** variable is a factor with the following 3 levels: 
**ctrl**, **trt1**, **trt2**.


* It is appropriate to make the **group** variable in **PlantGrowth** 
a **factor** since this variable represents the treatment condition in this study.

* Because the **levels** of group (**ctrl**, **trt1**, **trt2**) represent the collection of possible values,
you **cannot** assign the elements of **PlantGrowth$group** a value 
which is not either **ctrl**, **trt1**, or **trt2**.

```r
PlantGrowth$group[4] <- "trt" 
```

```
## Warning in `[<-.factor`(`*tmp*`, 4, value = structure(c(1L, 1L, 1L, NA, :
## invalid factor level, NA generated
```

* Assigning the 5th element the value `"trt1"` works though:

```r
PlantGrowth$group[5] <- "trt1" 
```


---


* The other **main attribute** which distinguishes factors is its **class**.

```r
attr(PlantGrowth$group, "class")  # Check the class attribute
```

```
## [1] "factor"
```

* If the **class** of a vector is a **factor**, numerical comparisons
between elements will return an error:

```r
PlantGrowth$group[5] > PlantGrowth$group[15]
```

```
## Warning in Ops.factor(PlantGrowth$group[5], PlantGrowth$group[15]): '>' not
## meaningful for factors
```

```
## [1] NA
```


```r
PlantGrowth$group[5] + PlantGrowth$group[15] # This returns an error
```

```
## Warning in Ops.factor(PlantGrowth$group[5], PlantGrowth$group[15]): '+' not
## meaningful for factors
```

```
## [1] NA
```


## Adding new levels to a factor

* In some cases, you want to **add data 
to a factor vector**, and the new data contains new
categories which are not in the original factor vector.
  
* To do this, you can assign **new levels** to your factor 
vector by using the assignment:

```r
`levels(vec_name) <- `
```

* For example, look what happens when we try to change the 
value of one element from a factor vector

```r
y <- factor(rep(1:3, 3)) # create factor with levels 1, 2, 3
y[3] <- 4  # Try to assign 3rd element the value 4
```

```
## Warning in `[<-.factor`(`*tmp*`, 3, value = 4): invalid factor level, NA
## generated
```

```r
y  # Note that the third element is now NA
```

```
## [1] 1    2    <NA> 1    2    3    1    2    3   
## Levels: 1 2 3
```


* We **can add** the value $4$ to this vector, but we need to change
the **factor levels** first:

```r
levels(y) <- c(1,2,3,4)
y[3] <- 4
y
```

```
## [1] 1 2 4 1 2 3 1 2 3
## Levels: 1 2 3 4
```

---

* The `str()` function gives a description of any **R** object.

* For a data frame, you can see which variables are treated as **factors**
and which are treated as **numeric**


```r
str( PlantGrowth )
```

```
## 'data.frame':	30 obs. of  2 variables:
##  $ weight: num  4.17 5.58 5.18 6.11 4.5 4.61 5.17 4.53 5.33 5.14 ...
##  $ group : Factor w/ 3 levels "ctrl","trt1",..: 1 1 1 NA 2 1 1 1 1 1 ...
```





## The table() function

* The `table()` function can be used to count the **number of observations** at 
each **level** of a factor.

* `table()` can also be used to count the number of observations
ocurring at each .**level combination** for **2 or more factors**.

* For example, let's count the number of observations in each treatment 
group in the **PlantGrowth** data:

```r
table( PlantGrowth$group ) # 10 observations in each group
```

```
## 
## ctrl trt1 trt2 
##   10   10   10
```

---

* To see how **table** works for multiple factors, let's look at
the **VA** dataset from the **MASS** package

```r
library(MASS)
data(VA)  # load the VA data frame
str(VA)  # look at the structure of this data frame
```

```
## 'data.frame':	137 obs. of  8 variables:
##  $ stime    : num  72 411 228 126 118 10 82 110 314 100 ...
##  $ status   : num  1 1 1 1 1 1 1 1 1 0 ...
##  $ treat    : Factor w/ 2 levels "1","2": 1 1 1 1 1 1 1 1 1 1 ...
##  $ age      : num  69 64 38 63 65 49 69 68 43 70 ...
##  $ Karn     : num  60 70 60 60 70 20 40 80 50 70 ...
##  $ diag.time: num  7 5 3 9 11 5 10 29 18 6 ...
##  $ cell     : Factor w/ 4 levels "1","2","3","4": 1 1 1 1 1 1 1 1 1 1 ...
##  $ prior    : Factor w/ 2 levels "0","10": 1 2 1 2 2 1 2 1 1 1 ...
```


* Notice that the variables **treat** and **cell** are **factors** in the **VA** data frame.

* You can **cross-tabulate** these two factors by using plugging both variables into the **table** function.

```r
tab.VA <- table(VA$treat, VA$cell)
tab.VA
```

```
##    
##      1  2  3  4
##   1 15 30  9 15
##   2 20 18 18 12
```

* **tab.VA** is an example of what's usually called a 2x4 **contingency table.**

* You can compute the table margins as if **tab.VA** were a matrix

```r
colSums(tab.VA)
```

```
##  1  2  3  4 
## 35 48 27 27
```


* You are not limited to cross-tabulating two factor variables.

* For example, we can cross-tabulate the factors **treat**, **cell**, and **prior**:

```r
table(VA$treat, VA$cell, VA$prior)
```

```
## , ,  = 0
## 
##    
##      1  2  3  4
##   1  8 23  7 10
##   2 13 14 15  7
## 
## , ,  = 10
## 
##    
##      1  2  3  4
##   1  7  7  2  5
##   2  7  4  3  5
```

* This outputs **two** 2x4 contingency tables: A contingency table of **treat** and **cell** for 
each level of **prior**.


## tapply() and aggregate

* `tapply()` is useful when you want to compute
certain summary statistics **for each** level of a factor variable.

* For example, suppose we wanted to compute 
the **mean** and **standard deviation** of 
**age** in the **VA** data within each treatment group.

* This can be done with the following code:

```r
tapply(VA$age, VA$treat, mean) # compute mean age in each trt. group
```

```
##        1        2 
## 57.50725 59.11765
```

```r
tapply(VA$age, VA$treat, sd)  # compute sd of age in each trt. group
```

```
##        1        2 
## 10.81070 10.27754
```


* You can use the `aggregate()` function to 
use `tapply()` across multiple variables.

* This is useful, for example, if you want to compute
the mean of **each** of the numeric variables in a data frame
using a single command.

* Note that the variables **stime**, **status**, **age**, **Karn**,
**diag.time** in the **VA** data are numeric:

```r
str(VA)
```

```
## 'data.frame':	137 obs. of  8 variables:
##  $ stime    : num  72 411 228 126 118 10 82 110 314 100 ...
##  $ status   : num  1 1 1 1 1 1 1 1 1 0 ...
##  $ treat    : Factor w/ 2 levels "1","2": 1 1 1 1 1 1 1 1 1 1 ...
##  $ age      : num  69 64 38 63 65 49 69 68 43 70 ...
##  $ Karn     : num  60 70 60 60 70 20 40 80 50 70 ...
##  $ diag.time: num  7 5 3 9 11 5 10 29 18 6 ...
##  $ cell     : Factor w/ 4 levels "1","2","3","4": 1 1 1 1 1 1 1 1 1 1 ...
##  $ prior    : Factor w/ 2 levels "0","10": 1 2 1 2 2 1 2 1 1 1 ...
```


* We can compute the mean of each of the numeric variables in 
**VA**, stratified by cell type, by using `aggregate()` in the following way:

```r
# Use aggregate on VA only using 1st, 2nd, 4th, 5th, 6th variables
aggregate(VA[,c(1,2,4,5,6)], list(VA$cell), mean)
```

```
##   Group.1     stime    status      age     Karn diag.time
## 1       1 200.20000 0.8857143 58.45714 60.85714 11.028571
## 2       2  71.66667 0.9375000 59.87500 53.54167  9.250000
## 3       3  64.11111 0.9629630 57.40741 58.11111  5.629630
## 4       4 166.11111 0.9629630 56.22222 65.00000  8.148148
```

* Compute the **median** of each of the variables stratified by cell type

```r
aggregate(VA[,c(1,2,4,5,6)], list(VA$cell), median)
```

```
##   Group.1 stime status  age Karn diag.time
## 1       1   111      1 62.0   60         7
## 2       2    51      1 62.5   60         4
## 3       3    51      1 61.0   60         4
## 4       4   156      1 62.0   70         8
```
