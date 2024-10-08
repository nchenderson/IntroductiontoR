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


```r
library(nycflights13)
```



```r
data(flights)
```


```r
flights <- as.data.frame( flights )
```




