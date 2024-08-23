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
