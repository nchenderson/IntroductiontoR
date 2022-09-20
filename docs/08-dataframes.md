# Data Frames {#dataframe}



|     Dimension     |         Homogeneous         |   Heterogeneous   |
|:-----------------:|:---------------------------:|:-----------------:|
|    1-Dimension    |        Atomic Vector        |       List        |
|    2-Dimension    |           Matrix            |    Data Frame     |
|   >2-Dimensions   |   Multi-dimensional array   |                   |

* **Data Frames** are the most common tool for storing "rectangular" datasets (data stored as a table in rows and columns) in **R**.
    + Each row holds an **observation**.
    + Each column holds a **variable**.

* Roughly speaking, a data frame can be thought of as a matrix where 
**different columns** can hold **different types** of data.
    + The elements in the **same column** of a data frame should have the **same type**. 


* More technically, a data frame is actually a .red[list of vectors] that all 
have the same length. **Number of variables = number of elements in list.**

---

* Let's first look at one of **R's** built-in datasets to see an example of a data frame.

* **R** has many **built-in datasets** that are stored as data frames.

* Type in `library(help = "datasets")` to see the full list of built-in
datasets.

* One of the built-in datasets is the **PlantGrowth** dataset.

* You can **load** this dataset into your **R** session by typing in

```r
data(PlantGrowth)
```

* Check that `PlantGrowth` is a data frame by using

```r
class(PlantGrowth)
```

```
## [1] "data.frame"
```

---

* You can display the first few rows of the **PlantGrowth** data by using `head()`:

```r
head( PlantGrowth )
```

```
##   weight group
## 1   4.17  ctrl
## 2   5.58  ctrl
## 3   5.18  ctrl
## 4   6.11  ctrl
## 5   4.50  ctrl
## 6   4.61  ctrl
```

* This dataset has **30 observations** and **2 variables**.
    + This can be seen by applying `dim()` to the data frame: 

```r
dim( PlantGrowth )
```

```
## [1] 30  2
```


## Creating Data Frames

* The main way to **create** a data frame in R is to use the function `data.frame`.

* To create a data frame with 5 observations and two variables named **x** and **y**:

```r
# x and y have to be the same length
df <- data.frame(x=c(1,2,3,4,5), y=c(1,4,9,16,25))
df
```

```
##   x  y
## 1 1  1
## 2 2  4
## 3 3  9
## 4 4 16
## 5 5 25
```

* **Converting** a data frame to a matrix


```r
df.mat <- as.matrix(df) ## How a Data Frame looks like  
df
```

```
##   x  y
## 1 1  1
## 2 2  4
## 3 3  9
## 4 4 16
## 5 5 25
```

```r
df.mat  ## How a matrix looks like
```

```
##      x  y
## [1,] 1  1
## [2,] 2  4
## [3,] 3  9
## [4,] 4 16
## [5,] 5 25
```


* You can use `as.data.frame` to convert a matrix into a data frame. 


```r
X <- matrix(1:6,3,2) 
colnames(X) <- c("a","b")
X.df <- as.data.frame(X)
X
```

```
##      a b
## [1,] 1 4
## [2,] 2 5
## [3,] 3 6
```

```r
X.df
```

```
##   a b
## 1 1 4
## 2 2 5
## 3 3 6
```

* Remember that a data frame can take **heterogeneous** data types.

```r
df <- data.frame(x=c(1,2,3),y=c("a","a","bc"))
colnames(X) <- c("a","b")
X.df <- as.data.frame(X)
X
```

```
##      a b
## [1,] 1 4
## [2,] 2 5
## [3,] 3 6
```

```r
X.df
```

```
##   a b
## 1 1 4
## 2 2 5
## 3 3 6
```


## Accessing and Modifying Data Frames

* One way to **access** the individual elements of a data frame is by specifying the row/column index. 
    + This is done in exactly the **same way** as with a **matrix**.


```r
df[,1]   ## access a column just like a matrix
```

```
## [1] 1 2 3
```

```r
df[1:2,] ## access rows like matrix
```

```
##   x y
## 1 1 a
## 2 2 a
```

```r
df[2, 1] ## access individual elements
```

```
## [1] 2
```


* You can access the data from a specific variable **by name** 
using the syntax: `df_name$var_name`.


```r
df$y   ## access a column by name
```

```
## [1] "a"  "a"  "bc"
```

```r
       ## what happens if we omit a comma?
df[1]  ## (Remember that df is actually list)
```

```
##   x
## 1 1
## 2 2
## 3 3
```


* Differences in element access between matrices and data frames:

```r
df.mat <- as.matrix(df) 
df[2] #df[10] will not work
```

```
##    y
## 1  a
## 2  a
## 3 bc
```

```r
df.mat[2]
```

```
## [1] "2"
```

```r
df.mat[10]
```

```
## [1] NA
```


* **Modifying** data frames:


```r
df <- data.frame(x=c(1,2,3),y=c("a","a","bc")) 
df$z = c("def","123","123") ## adding a new column
df
```

```
##   x  y   z
## 1 1  a def
## 2 2  a 123
## 3 3 bc 123
```

```r
df2 <- data.frame(w=c(TRUE,FALSE,FALSE))
cbind(df,df2)  # combine columns
```

```
##   x  y   z     w
## 1 1  a def  TRUE
## 2 2  a 123 FALSE
## 3 3 bc 123 FALSE
```


* **Adding** new rows to a data frame:

```r
df3 <- data.frame(x=4,y="a",z="def") 
rbind(df,df3)  
```

```
##   x  y   z
## 1 1  a def
## 2 2  a 123
## 3 3 bc 123
## 4 4  a def
```


## Subsetting data frames


```r
df
```

```
##   x  y   z
## 1 1  a def
## 2 2  a 123
## 3 3 bc 123
```

```r
subset(df, x>1)
```

```
##   x  y   z
## 2 2  a 123
## 3 3 bc 123
```

```r
subset(df, x>1 & y =="a")  
```

```
##   x y   z
## 2 2 a 123
```

## Exercises

1. For this exercise, you will use the `Loblolly` dataset which is a built-in **R** dataset.  You can load the `Loblolly` data frame and look at the first few rows with the following \textbf{R} commands: 

```r
data(Loblolly)
head(Loblolly)
```
+ In `Loblolly`, each different value of the variable `Seed` variable corresponds to a different tree.
    + How many rows are in the `Loblolly` data frame?
    + What is the **mean** and **standard deviation** of the `age` variable in `Loblolly`?
    + How many of the values in the variable `height` are greater than $50$ feet?
    + What is the correlation between the `height` and `age` variables? (For this part, you can use the `cor` function)
    + Add a variable called `Seed.first` to the `Loblolly` data frame. This 
variable should equal $1$ at the **first** occurrence of a value of **Seed** 
and equal $0$ if the value of **Seed** is already in a previous row of `Loblolly`. 
    + How many different trees (i.e., unique values of the `Seed` variable) are there in this data frame?
    + Add another variable called `obs.num` to the `Loblolly` data frame. This
variable should equal $1$ the first time a value of `Seed` occurs, should equal $2$ the second time a value of `Seed` occurs, etc. ...
    + Add another variable to `Loblolly` called `height.change` which measures 
the change in height from the earliest age of the tree to the latest age of the tree. After completing steps (a)-(h), the first 8 rows your modified `Loblolly` data frame should look like the following ... 
    + Compute a vector which contains the "within-tree" correlations between `height` and `age`. The $k^{th}$ element of this vector should contain the correlation between the height and age values from the $k^{th}$ tree.

2. Create a data frame with the following variables:
    + **x** a numeric variable equal to 1:12
    + **y** a numeric variable equal to **x^2**
    + **z** a character variable with elements: "a", "b", "c", "a", "b", "c", ....
    + Compute the mean of **y** only for those observations where **z == "a"**.
    + Compute the mean of **x** only for those observations where
**both** **x > 5** and **z==a**.
    + Change the 10th element of the **z** variable to "d".
    + Create a subset of this data frame for observations where **x** is even.

