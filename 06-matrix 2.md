# Matrices in R {#matrix}

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


## Creating a matrices in R

* The most common way to create a matrix is 
with the **matrix** function.

* The form of the **matrix** function is

```r
matrix(x, nrow, ncol)
```

* **x** is a **vector** that you want to convert into a matrix.
    + `nrow` is the number of rows you want the matrix to have.
    
    + `ncol` is the number of columns you want the matrix to have.

    + `x` could be a single number (a vector of length one) in which 
      case the returned matrix will have all the same entries. 


* If we wanted to create a matrix named `A` with **2 rows** and **3 columns** that contains
**only zeros**, we could use the following code

```r
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

```r
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

```r
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

```r
D <- matrix(x, 2, 3, byrow=TRUE)
D
```

```
##      [,1] [,2] [,3]
## [1,]    1    2    3
## [2,]    4    5    6
```


