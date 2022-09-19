# Data Wrangling {#datawrangling}

* **Data Wrangling** just refers to 
the process of organizing your data into a useful format so 
that you can 
    + Perform the **statistical analysis** you are interested in.
    
    + Produce the **data visualizations** you are interested in.

* The amount of work involved in the data wrangling process will
vary a lot depending on how **"clean"** the original dataset is. 

* Examples of steps involved in data wrangling:
    + **subsetting data**,
    + **merging data**, 
    + **transforming data**, 
    + **deriving new variables**,
    + **handling missing data**

## The nycflights13 data

* To illustrate the techniques described in this chapter, we will use the **"NYC Flights Dataset"** available from the `nycflights13` **R** package.

* To load this package into **R**, first install the `nycflights13` and 
then load it into **R** with the following command:

```r
library(nycflights13)
```

* This package has several datasets available.

* We will explore the `flights` dataset in this chapter. 
    + This dataset can be loaded into **R** with the following command.

```r
data(flights)
```

* tibble vs. data frame here.

```r
flights <- as.data.frame( flights )
```

## Exploring the Dataset

* The first thing you usually want to note about a dataset after first loading it is **how many observations** and **variables** there are.

* While you can note the dimensions of your data under the **"Environment"** tab in Rstudio, you can see this by using `dim`

```r
dim(flights)
```

```
## [1] 336776     19
```

* This data frame has $336,776$ observations and $19$ variables.

* To see what is stored in the **first few rows** of `flights` use `head`:

```r
head(flights)
```

```
##   year month day dep_time sched_dep_time dep_delay arr_time sched_arr_time
## 1 2013     1   1      517            515         2      830            819
## 2 2013     1   1      533            529         4      850            830
## 3 2013     1   1      542            540         2      923            850
## 4 2013     1   1      544            545        -1     1004           1022
## 5 2013     1   1      554            600        -6      812            837
## 6 2013     1   1      554            558        -4      740            728
##   arr_delay carrier flight tailnum origin dest air_time distance hour minute
## 1        11      UA   1545  N14228    EWR  IAH      227     1400    5     15
## 2        20      UA   1714  N24211    LGA  IAH      227     1416    5     29
## 3        33      AA   1141  N619AA    JFK  MIA      160     1089    5     40
## 4       -18      B6    725  N804JB    JFK  BQN      183     1576    5     45
## 5       -25      DL    461  N668DN    LGA  ATL      116      762    6      0
## 6        12      UA   1696  N39463    EWR  ORD      150      719    5     58
##             time_hour
## 1 2013-01-01 05:00:00
## 2 2013-01-01 05:00:00
## 3 2013-01-01 05:00:00
## 4 2013-01-01 05:00:00
## 5 2013-01-01 06:00:00
## 6 2013-01-01 05:00:00
```

---

* You can use `str` to see which variables are stored as **numeric** vs. **character** vs. **factor**.
    + In many cases, you may want to change the character variables to factor.
    
    + You may notice that one of the variables in this dataset has the `POSIXct` type which is a special data type used to store times.


```r
str(flights)
```

```
## 'data.frame':	336776 obs. of  19 variables:
##  $ year          : int  2013 2013 2013 2013 2013 2013 2013 2013 2013 2013 ...
##  $ month         : int  1 1 1 1 1 1 1 1 1 1 ...
##  $ day           : int  1 1 1 1 1 1 1 1 1 1 ...
##  $ dep_time      : int  517 533 542 544 554 554 555 557 557 558 ...
##  $ sched_dep_time: int  515 529 540 545 600 558 600 600 600 600 ...
##  $ dep_delay     : num  2 4 2 -1 -6 -4 -5 -3 -3 -2 ...
##  $ arr_time      : int  830 850 923 1004 812 740 913 709 838 753 ...
##  $ sched_arr_time: int  819 830 850 1022 837 728 854 723 846 745 ...
##  $ arr_delay     : num  11 20 33 -18 -25 12 19 -14 -8 8 ...
##  $ carrier       : chr  "UA" "UA" "AA" "B6" ...
##  $ flight        : int  1545 1714 1141 725 461 1696 507 5708 79 301 ...
##  $ tailnum       : chr  "N14228" "N24211" "N619AA" "N804JB" ...
##  $ origin        : chr  "EWR" "LGA" "JFK" "JFK" ...
##  $ dest          : chr  "IAH" "IAH" "MIA" "BQN" ...
##  $ air_time      : num  227 227 160 183 116 150 158 53 140 138 ...
##  $ distance      : num  1400 1416 1089 1576 762 ...
##  $ hour          : num  5 5 5 5 6 5 6 6 6 6 ...
##  $ minute        : num  15 29 40 45 0 58 0 0 0 0 ...
##  $ time_hour     : POSIXct, format: "2013-01-01 05:00:00" "2013-01-01 05:00:00" ...
```

---

* Each row of `flights` holds information related to a **single flight** that departed from the New York City area in 2013.

* The `carrier` variable in `flights` contains the abbreviation for the airline carrier. 

* We can see that there are 16 **different carriers** in this dataset by using `unique`:

```r
length( unique(flights$carrier) )  ## 16 unique carriers
```

```
## [1] 16
```

* Each plane has a unique **tail number**. Using `unique`, we can see that 
there are $4044$ unique planes represented in the `flights` dataset

```r
length( unique(flights$tailnum) )
```

```
## [1] 4044
```

* Using `table`, we can see which **carriers** had the most flights out of the New York City area:

```r
table( flights$carrier )
```

```
## 
##    9E    AA    AS    B6    DL    EV    F9    FL    HA    MQ    OO    UA    US 
## 18460 32729   714 54635 48110 54173   685  3260   342 26397    32 58665 20536 
##    VX    WN    YV 
##  5162 12275   601
```

## Summarizing each variable



## Using the dplyr package

