# Lists {#list}

* R always store data as a **"collection"**.


|     Dimension     |         Homogeneous         |   Heterogeneous   |
|:-----------------:|:---------------------------:|:-----------------:|
|    1-Dimension    |        Atomic Vector        |       List        |
|    2-Dimension    |           Matrix            |    Data Frame     |
|   >2-Dimensions   |   Multi-dimensional array   |                   |
* There is no "0-dimensional data" in R.

* Even a single-valued object, it is considered as a "vector" with size 1

Source: http://adv-r.had.co.nz/Data-structures.html 


## Creating Lists in R

* Lists can store a collection of items that have **different types**.

* To **create a list**, you can use the `list` function. 


```r
## Use a keyword argument to define any attribute of any data type
emp_info <- list(name="Nicholas Henderson", UMID=12345678, 
                 faculty=TRUE)
emp_info # list has character, numeric, and logical types
```

```
## $name
## [1] "Nicholas Henderson"
## 
## $UMID
## [1] 12345678
## 
## $faculty
## [1] TRUE
```

```r
emp_info$name # access components with $component_name
```

```
## [1] "Nicholas Henderson"
```


* Create a list with **named components**: **a**, **b**, and **d**.


```r
list(a=c(1,2,3), b=c("apple","banana"),
     d=TRUE) ## list elements can be vectors
```

```
## $a
## [1] 1 2 3
## 
## $b
## [1] "apple"  "banana"
## 
## $d
## [1] TRUE
```


## Accessing list elements

* You can create **named lists** or **unnamed lists**.
    + In an **unnamed list**, the list components **do not** have names.

* You can access the $k^{th}$ element of an **unnamed list** using 
the double bracket syntax `[[k]]`.

---

* You can access the elements of a **named list** using either the 
indexing `[[k]]` or the component names.


```r
# Create an unnamed list and look at the first element:
y <- list(c(1,2,3), c("apple","banana"), TRUE)  
y[[1]]  
```

```
## [1] 1 2 3
```

---

* Accessing the elements of a named list using 
either the **numeric index** or the **component names**:

```r
x <- list(a=c(1,2,3), b=c("apple", "banana"), d=TRUE) 
x$a
```

```
## [1] 1 2 3
```

```r
x[[1]]
```

```
## [1] 1 2 3
```

```r
x$b
```

```
## [1] "apple"  "banana"
```

```r
x[[2]]
```

```
## [1] "apple"  "banana"
```


## Working with lists

* Get the names of the list components by using `names(list_name)`

```r
names(x)
```

```
## [1] "a" "b" "d"
```

* Find the length of a list by using `length`.
    + Note that the length of a list is the **number of components** of the list,
    and the length does not depend on the length of any of the vector components.
    

```r
length(x)
```

```
## [1] 3
```



### Expanding a list: adding more components

* Add components to a list using either the index or by name

```r
x
```

```
## $a
## [1] 1 2 3
## 
## $b
## [1] "apple"  "banana"
## 
## $d
## [1] TRUE
```

```r
x[[4]] <- 4
x$e <- 5
```


```r
x
```

```
## $a
## [1] 1 2 3
## 
## $b
## [1] "apple"  "banana"
## 
## $d
## [1] TRUE
## 
## [[4]]
## [1] 4
## 
## $e
## [1] 5
```


##  When are lists useful?

* Many **R** functions return **multiple** items as output. 
    + It is common to return these multiple items in a single, **named list**. 
    

```r
matrixSum <- function(X) { # calculate possible sums of a matrix
  s1 <- rowSums(X)
  s2 <- colSums(X)
  s3 <- sum(X)
  return(list(row=s1, col=s2, all=s3)) ## return multiple values 
                                       ## using a list
}

A <- matrix(1:6,2,3)
matrixSum(A)
```

```
## $row
## [1]  9 12
## 
## $col
## [1]  3  7 11
## 
## $all
## [1] 21
```



* Lists are **useful** in situations where you have a collection of items 
of **different types** and **dimensions** that you want
to store in a single **"variable"**.

* For example, you may have data on several individuals
where, **for each individual**, you have data stored 
in a vector, a matrix, and a data frame.



## lapply(): Applying functions to lists

* **lapply** ("list apply") works like an **apply()** function
for **lists**.

* **lapply** has two arguments:
    + An input **list**.
    + The **name** of the **function** to apply to each component of the list.

* **lapply** returns a list with the **same number** of components as the input list:

```r
r <- matrixSum(A) # r is a list with 3 components.
lapply(r, length) # compute the length of each component of r
```

```
## $row
## [1] 2
## 
## $col
## [1] 3
## 
## $all
## [1] 1
```



```r
lapply(r, sum) # Compute sum of each component of r
```

```
## $row
## [1] 21
## 
## $col
## [1] 21
## 
## $all
## [1] 21
```

```r
lapply(r, function(x) sum(x*x)) # Compute sum of squares for each component
```

```
## $row
## [1] 225
## 
## $col
## [1] 179
## 
## $all
## [1] 441
```


### Use sapply() for simpler output

* When applying a function to **each** component of a list,
it is often preferable to have the **result** returned as a **vector**
or **matrix** instead of a list.

* This is what the **sapply()** ("simplified lapply") function does.


```r
sapply(r, sum) # sapply() returns output as a named vector
```

```
## row col all 
##  21  21  21
```

```r
lapply(r,sum)
```

```
## $row
## [1] 21
## 
## $col
## [1] 21
## 
## $all
## [1] 21
```


* If the **function** used in **sapply** returns a vector 
with length **longer** than 1, **sapply** will return a matrix.


```r
r
```

```
## $row
## [1]  9 12
## 
## $col
## [1]  3  7 11
## 
## $all
## [1] 21
```

```r
                                ## column names of matrix are same
sapply(r, function(x) c(min(x),max(x)) ) ## as list component names
```

```
##      row col all
## [1,]   9   3  21
## [2,]  12  11  21
```



## Exercises

1. Suppose we define the vector `x` as `x <- c(1,2,3)`. What is the value of 

```r
length( list(x) ) == length(x)
```

2. Write a function that takes a **list** called **x** as input, and the elements of `x` can be assumed to be numeric vectors. The function should **return** a matrix where
    + the **number of columns** of the matrix equal the number of elements of the input list.
    + the **number of rows**of the matrix equals 4
    + If the $k^{th}$ element of the list has length greater than 4, 
the $k^{th}$ column of the output matrix should be `(mean(x[[k]]), median(x[[k]]), min(x[[k]]), max(x[[k]]))`
    + If the $k^{th}$ element of the list has length 4 or less, the 
$k^{th}$ column of the output matrix should be `(0, 0, 0, 0)`.




