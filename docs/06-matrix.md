# Matrices {#matrix}

* A **matrix** is a table of data organized into **rows** and **columns**. 
\begin{equation}
\mathbf{A} = \begin{bmatrix} a_{11} & a_{12} & \ldots & a_{1p} \\
a_{21} & a_{22} & \ldots & a_{2p} \\
\vdots & \vdots & \ddots & \vdots \\
a_{n1} & a_{12} & \ldots & a_{np}
\end{bmatrix} \nonumber
\end{equation}

* The matrix $\mathbf{A}$ has $n$ rows and $p$ columns.
    
* The matrix element $a_{ij}$ represents the number in the $i^{th}$ row and $j^{th}$ column.

* **R** allows the elements of a matrix to be **any type**.

* As with vectors, the **elements** of a matrix in **R** must all have the **same type**.


## Creating matrices in R

* The most common way to create a matrix is 
with the **matrix** function.

* The form of the **matrix** function is

``` r
matrix(x, nrow, ncol)
```

* **x** is a **vector** that you want to convert into a matrix.
    + `nrow` is the number of rows you want the matrix to have.
    
    + `ncol` is the number of columns you want the matrix to have.

    + `x` could be a single number (a vector of length one) in which 
      case the returned matrix will have all the same entries. 


* If we wanted to create a matrix named `A` with **2 rows** and **3 columns** that contains
**only zeros**, we could use the following code

``` r
A <- matrix(0, 2, 3) 
A
```

```
##      [,1] [,2] [,3]
## [1,]    0    0    0
## [2,]    0    0    0
```

* To **convert** a vector into a matrix 

* **Convert** the vector (1, 2, 3, 4, 5, 6) into a matrix with 2 rows and 3 columns

``` r
x <- 1:6     # x is a vector of 1,2,3,4,5,6 
B <- matrix(x, 2, 3) # create a matrix from this vector
B
```

```
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```


* Notice that **matrix** function fills in the matrix entries by columns (i.e, it fills in the numbers from `x` in the first column, then moves to the second, etc.)
   + This is referred to as filling in the entries "**by column**"

``` r
x <- 1:6     # x is a vector of 1,2,3,4,5,6 
B <- matrix(x, 2, 3) # create a matrix from this vector
B
```

```
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```

* You can instead fill in the matrix entries **by rows** by using the **keyword** argument `byrow = TRUE`

``` r
D <- matrix(x, 2, 3, byrow=TRUE)
D
```

```
##      [,1] [,2] [,3]
## [1,]    1    2    3
## [2,]    4    5    6
```

---


* It is often useful to create a matrix which has **all the same** columns (or rows):

``` r
matrix(1:2, 2, 3) # duplicates the column vector c(1,2)
```

```
##      [,1] [,2] [,3]
## [1,]    1    1    1
## [2,]    2    2    2
```

``` r
matrix(1:3, 2, 3) # this does not duplicate the row vector c(1,2,3)
```

```
##      [,1] [,2] [,3]
## [1,]    1    3    2
## [2,]    2    1    3
```

``` r
matrix(1:3, 2, 3, byrow=TRUE) # but this one does!
```

```
##      [,1] [,2] [,3]
## [1,]    1    2    3
## [2,]    1    2    3
```

## Accessing different features of a matrix

### Accessing elements of a matrix

* To access the $(i,j)$ **element** of a matrix `A`, use the syntax `A[i,j]`

* As an example of this, let's create a $2 \times 3$ matrix `A` and look at the $(2,1)$ element of `A`:

``` r
A <- matrix(1:6, 2, 3, byrow=TRUE) # creating a 2x3 matrix
A                         # print the matrix
```

```
##      [,1] [,2] [,3]
## [1,]    1    2    3
## [2,]    4    5    6
```

``` r
A[2,1]
```

```
## [1] 4
```

* You can access different subsets of a matrix by using vectors of indeces rather than single numbers in the indexing bracket.

* For example, if you want to look at elements $(2, 1)$ and $(2,2)$ of `A`, you can use the following syntax:

``` r
A[2,1:2]
```

```
## [1] 4 5
```

* Similarly, if you want to access all elements of `A` in either the first two rows or first two columns of `A`, you can use the following syntax:

``` r
A[1:2, 1:2]
```

```
##      [,1] [,2]
## [1,]    1    2
## [2,]    4    5
```

* To access the entire **kth column** of `A`, use the syntax `A[,k]`.
     + To access the entire **kth row** of `A`, use the syntax `A[k,]`

``` r
A[,2]  ## access 2nd column of A
```

```
## [1] 2 5
```
     
     





---

* Using **nrow()** or **ncol()** let you see the number of 
**rows** or **columns** of a matrix.

``` r
A <- matrix(1:6, 2, 3, byrow=TRUE) # creating a 2x3 matrix

nrow(A)
```

```
## [1] 2
```

``` r
ncol(A)
```

```
## [1] 3
```

* **dim** will return **both** the number of rows and columns.


``` r
dim(A)
```

```
## [1] 2 3
```

---


* While using the `A[i,j]` syntax is a more typical way of accessing specific elements of a matrix, you can **also** access the elements of a matrix as you would with a **vector**. 

* For a matrix, the indexing increases **by column**
    + For example, if `A` has 3 rows: 
    + `A[1]=A[1,1]`, `A[2]=A[2,1]`, `A[3]=A[3,1]`, `A[4]=A[1,2]`, ...

* For example if we access the "4th" and "5th" elements of a $2 x 3$
matrix

``` r
A 
```

```
##      [,1] [,2] [,3]
## [1,]    1    2    3
## [2,]    4    5    6
```

``` r
A[4:5]          ## accessing like a one-dimensional vector
```

```
## [1] 5 3
```

* I don't really use this way of accessing matrix elements much though, 
in some cases, it is more convenient (e.g., `A[ which(A > 3) ]`)

---

* You can also access elements of a matrix **like a vector** using **logical subsetting**


``` r
which( A > 3)      ## getting indices with which
```

```
## [1] 2 4 6
```

``` r
A[ which(A>3) ]   ## getting the elements greater than 3
```

```
## [1] 4 5 6
```

### Diagonals of Matrices

* The **diagonals** of a matrix are the elements of the matrix where
the **row index** equals the **column index**.

* In a **diagonal matrix**, all **non-diagonal** elements must be zero.

* To create a **diagonal** matrix in **R**, use the `diag` function.
    + You must provide the vector of **diagonal elements** as the input to `diag`

``` r
diag(1:4)   # 4x4 diagonal matrix with (1,2,3,4) as diagonals
```

```
##      [,1] [,2] [,3] [,4]
## [1,]    1    0    0    0
## [2,]    0    2    0    0
## [3,]    0    0    3    0
## [4,]    0    0    0    4
```


* If you use `diag(A)` where the **input** argument `A` is a **matrix**, this 
will return the **diagonal elements** of `A`.


``` r
A <- matrix (1:9, 3, 3)
A
```

```
##      [,1] [,2] [,3]
## [1,]    1    4    7
## [2,]    2    5    8
## [3,]    3    6    9
```

``` r
diag(A)   # returns diagonals of this matrix
```

```
## [1] 1 5 9
```

---

* Working with **off-diagonal** elements.

* The function `upper.tri(A)` returns a **logical matrix** of the same dimension as `A` with `TRUE` values on the "upper diagonal" part of the matrix.
    + Thus, you can use `upper.tri` to update the upper diagonal parts of a matrix.


``` r
x <- matrix (1:9, 3, 3)
x[upper.tri(x)] <- 0
x
```

```
##      [,1] [,2] [,3]
## [1,]    1    0    0
## [2,]    2    5    0
## [3,]    3    6    9
```

* Similarly, `lower.tri(A)` allows you to look at the subset of entries on the "lower diagonal" part of a matrix. 

``` r
x[lower.tri(x,diag=TRUE)] <- 10:15
x
```

```
##      [,1] [,2] [,3]
## [1,]   10    0    0
## [2,]   11   13    0
## [3,]   12   14   15
```



### Naming rows or columns

* You can give a name to each row with the **rownames** function.
    + The collection of **row names** of a matrix should be a **vector**.


``` r
x <- matrix(1:6, nrow=2, ncol=3)
rownames(x) <-c("a","b")
x
```

```
##   [,1] [,2] [,3]
## a    1    3    5
## b    2    4    6
```

* You can actually access rows of a matrix **by name**:


``` r
x[1,] 
```

```
## [1] 1 3 5
```

``` r
rownames(x) <-c("a","b")
x["a",]
```

```
## [1] 1 3 5
```

* Similarly, you can access **columns** of a matrix **by name**:


``` r
colnames(x) <-c("c1","c2","c3") 
x
```

```
##   c1 c2 c3
## a  1  3  5
## b  2  4  6
```

``` r
x[2, c(2,3)]
```

```
## c2 c3 
##  4  6
```

``` r
x["b", c("c2","c3")]
```

```
## c2 c3 
##  4  6
```

### Combining rows or columns

* You can **"join"** matrices in "vertical" or "horizontal" ways
by using the functions 
   + `cbind` (**column** bind)
   + `rbind` (**row** bind)


``` r
X <- matrix(1:6,2,3)
Y <- X^2
cbind(X,Y)
```

```
##      [,1] [,2] [,3] [,4] [,5] [,6]
## [1,]    1    3    5    1    9   25
## [2,]    2    4    6    4   16   36
```

``` r
rbind(X,Y)
```

```
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
## [3,]    1    9   25
## [4,]    4   16   36
```



## Applying functions to matrices

* You can directly use **matrices** as input arguments with many of the widely-used built-in **R** functions.

* Functions like **sum** or **mean** will
take the sum (or average) of **all** 
the elements of a matrix:


``` r
A <- matrix (1:6, 2, 3)
sum(A)  # sum of all elements
```

```
## [1] 21
```

``` r
mean(A) # average of all elements
```

```
## [1] 3.5
```

``` r
sd(A)   # standard deviation of all elements
```

```
## [1] 1.870829
```


* You can take the **transpose** of a matrix `A` using `t(A)`.
    + You can **convert** a matrix `A` into a vector using `as.vector(A)` or simply `c(A)`.


``` r
A
```

```
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```

``` r
t(A)             ## transpose of A (reverse role of rows/columns)
```

```
##      [,1] [,2]
## [1,]    1    2
## [2,]    3    4
## [3,]    5    6
```

``` r
as.vector( A )   ## convert matrix to vector in column-wise order
```

```
## [1] 1 2 3 4 5 6
```

``` r
as.vector( t(A) ) ## convert matrix to vector in row-wise order
```

```
## [1] 1 3 5 2 4 6
```

### Mathematical operations with matrices

* Using `+,-,*,/` with two matrices performs **element-wise** addition,
subtraction, multiplication, and division.


``` r
y <- x <- matrix(1:6,2,3,byrow=TRUE)   
x + y  # matrix addition (element-by-element)
```

```
##      [,1] [,2] [,3]
## [1,]    2    4    6
## [2,]    8   10   12
```

``` r
x - y  # matrix subtraction (element-by-element)
```

```
##      [,1] [,2] [,3]
## [1,]    0    0    0
## [2,]    0    0    0
```

``` r
x*y  # element-wise multiplication
```

```
##      [,1] [,2] [,3]
## [1,]    1    4    9
## [2,]   16   25   36
```

* Note that `A*B` **does not** perform true matrix multiplication of matrices `A` and `B`.

* Matrix multiplication is done with `%*%` 


``` r
x %*% t(y)  # (2x3) x (3x2) matrix
```

```
##      [,1] [,2]
## [1,]   14   32
## [2,]   32   77
```

``` r
t(x) %*% y  # (3x2) x (2x3) matrix
```

```
##      [,1] [,2] [,3]
## [1,]   17   22   27
## [2,]   22   29   36
## [3,]   27   36   45
```


## Matrix Functionals

### Functions applied to **each** row/column

* We can take the **sum** or **mean** of each row/column of a matrix by using either `rowSums`, `rowMeans`, `colSums`, or `colMeans`.


``` r
A
```

```
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```

``` r
rowSums(A)
```

```
## [1]  9 12
```

``` r
colSums(A)
```

```
## [1]  3  7 11
```

``` r
rowMeans(A)
```

```
## [1] 3 4
```


* While `rowSums` works perfectly fine, let's try writing our own **rowSums()** function:

``` r
myRowSums <-function(x){
  ret <- rep(NA,nrow(x)) ## make an empty vector
  for(i in 1:nrow(x)) {
    ret[i] <-sum(x[i,])  ## take the sum of i-th row
  }
  return (ret)
}
rowSums(A)
```

```
## [1]  9 12
```

``` r
myRowSums(A)
```

```
## [1]  9 12
```


* The implementation by the function `myRowSums` works fine.

* However, it is a bit cumbersome to write such a function
whenever we want to compute **column-wise/row-wise** summary statistics.

* It would be nice if there were a **quick & general** way to do the following:
  + For **each** row or column of a matrix ...
  + Evaluate a **function** using the row/column vector as input
  + Return the collection of results as a **numeric vector**.
  

### **apply()**: dimension-wise aggregation



``` r
rowSums(A)    ## original row-wise sum
```

```
## [1]  9 12
```

``` r
apply(A, 1, sum) ## this also performs row-wise sum
```

```
## [1]  9 12
```

``` r
colSums(A)    ## original column-wise sum
```

```
## [1]  3  7 11
```

``` r
apply(A, 2, sum) ## this also performs column-wise sum
```

```
## [1]  3  7 11
```



* **First parameter** of apply: the **input matrix**.

* **Second parameter** of apply: the **dimension** over which to aggregate 
    + 1:rows,  2:columns

* **Third parameter** of apply: **function** to evaluate for each row/column


``` r
A
```

```
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```

``` r
apply(A, 1, sum)  # row sums
```

```
## [1]  9 12
```

``` r
apply(A, 2, sum)  # column sums
```

```
## [1]  3  7 11
```


* Examples of using apply:


``` r
colMeans(A)  ## original columnw-wise mean
```

```
## [1] 1.5 3.5 5.5
```

``` r
apply(A, 2, mean) ## same as above
```

```
## [1] 1.5 3.5 5.5
```

``` r
# colMax(A)   ## This will cause ERROR. colmax() does not exist!
apply(A, 2, max) ## But this works!
```

```
## [1] 2 4 6
```



### Using apply with your own function

* Suppose that instead of simply taking the row-wise or column-wise means we want to do the following:

* For **each** row/column:
  + Calculate the squared sum of each row/column.
  + Return the vector of squared sums.

* How can we do this using **apply()**?

---

* A **big** advantage of the **apply** function is the
**flexibility** it gives you.

* You can use **your own** functions to compute **row-wise/column-wise summary measures** for certain measures that may not be implemented in base **R**. 


``` r
## define a function named sqsum
sqsum <- function(x) {
  return( sum(x*x) )  ## very simple implementation
}
apply(A, 1, sqsum)    ## run sqsum() funciton
```

```
## [1] 35 56
```

---


* You can actually write the function definition **inside**
of the apply function.

* This can be convenient when using straightforward functions that can be written on a single line:

``` r
apply(A, 1, function(x) {return (sum(x*x))} )    ## much simpler!
```

```
## [1] 35 56
```

* Or, we can write the above apply statement in an even simpler form:


``` r
## You can omit return() and {} especially 
## for simple function definitions
apply(A, 1, function(x) sum(x*x) )    ## Even simpler!
```

```
## [1] 35 56
```

---

* **apply()** can also return a **matrix**


``` r
## if apply() returns a vector, each row stores results
apply(A, 1, function(x) c(min(x),max(x)) )
```

```
##      [,1] [,2]
## [1,]    1    2
## [2,]    5    6
```

``` r
apply(A, 2, function(x) c(min(x),max(x)) )
```

```
##      [,1] [,2] [,3]
## [1,]    1    3    5
## [2,]    2    4    6
```


## Exercises

1. Write a **function** that has two input arguments **A** and **B**
    + **A** and **B** are both matrices with the same dimension (same number of rows and columns).
    + The function returns a matrix **D**.
    + The `[i,j]` element of **D** should equal `A[i,j]` if `A[i,j] < B[i,j]` and equal `B[i,j]` if `A[i,j] >= B[i,j]`.
    + You can use either a **nested** for loop or **logical indexing**.
    
2. Suppose we define the matrix `X` as

``` r
X <- rbind( rep(c(1,4), each=3), rep(c(8,6), each=3))
```
What will be the value of `apply(X, 2, sum)[2]`?

3. Write a function called `PairwiseMedianDiffs` that
has **two numeric matrices** `A` and `B` as the input arguments. These two input matrices are assumed to have the same dimensions. This function should return a $p \times p$ matrix (where $p$ is the number of columns in `A`). The `[i,j]` element of the returned matrix should equal the median of the $i^{th}$ column of `A` minus the median of the $j^{th}$ column of `B`.

    
    
