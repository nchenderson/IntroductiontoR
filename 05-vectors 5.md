# (PART) R Data Structures {-}

# Vectors {#vectors}

* The most basic data type in **R** is the **vector**.

* As we mentioned previously, if we assign the number `42` to a 
variable named `x`, **R** will treat `x` as a vector.


```r
x <- 42  ## the x value is 42
x        ## print the value of x
```

```
## [1] 42
```

```r
x[1]     ## What does this do?
```

```
## [1] 42
```

* Here, `x` is considered to be a **vector** of length 1.

---

* Technically, there are two kinds of vectors in R: 
     + **atomic vectors**
     + **lists**
     
* However, it is very common to refer to **atomic vectors** as simply "**vectors**" and to refer to lists as "lists".

* Vectors that are **homogenous** (all elements have the same type) are technically referred to as **atomic vectors** in **R**.
    + It is common to refer to any atomic vector as a **vector**.
    + We will also refer to any atomic vector as a **vector**.

---

* R will always store data as a "**collection**".


|     Dimension     |         Homogeneous         |   Heterogeneous   |
|:-----------------:|:---------------------------:|:-----------------:|
|    1-Dimension    |        Atomic Vector        |       List        |
|   2-Dimensions    |           Matrix            |    Data Frame     |
|   >2-Dimensions   |   Multi-dimensional array   |                   |
* There is no "0-dimensional data" in R.

* Even a **single-valued object** is considered to be a "vector" with length 1.

Source: [http://adv-r.had.co.nz/Data-structures.html](http://adv-r.had.co.nz/Data-structures.html) 


## Creating vectors in R

### The concatenate function `c()`

* The most straightforward way to **create** vectors in **R** is to use the **concatenate** function `c()`

* This links together a group of values into a **single vector**.
    + You can also create a single vector from multiple vectors using `c`. 

* Examples of using `c()` to create numeric vectors are:

```r
x <- c(1,2,3) # create a length-3 vector with elements 1, 2, and 3
x
```

```
## [1] 1 2 3
```

```r
y <- c(x, 4, 5) # create a vector with elements 1,2,3,4,5
y
```

```
## [1] 1 2 3 4 5
```

---

* You are **not** limited to using numeric values with `c()`. 

* For example, you can use `c()` to create a vector of **characters or logicals**.

```r
char_vec <- c("cat", "dog", "hamster")  # vector of characters
char_vec
```

```
## [1] "cat"     "dog"     "hamster"
```

```r
log_vec <- c(TRUE, FALSE, TRUE, TRUE)  # vector of logicals
log_vec
```

```
## [1]  TRUE FALSE  TRUE  TRUE
```


### colon, seq, rep: Creating vectors with specific patterns

* It is often very useful to be able to create 
**vectors** with specific patterns.

* The **colon operator** `:` can be used to create
a sequence of numbers. 

* The code `from:end` will create a vector of numbers 
starting at `from` and increasing (or decreasing) by 1
until reaching `end`.

* Examples:

```r
x <- 1:5   # creates the vector (1,2,3,4,5)
x
```

```
## [1] 1 2 3 4 5
```

```r
y <- 22:28
y
```

```
## [1] 22 23 24 25 26 27 28
```

* You can also use the colon operator to create a **decreasing** sequence of numbers.

```r
z <- 0:-5 # use : to created decreasing vector
z   
```

```
## [1]  0 -1 -2 -3 -4 -5
```

* You can even have use a number with a **decimal point** as the **starting** 
or **ending** number (but this is not done that frequently).


```r
w <- 2.3:6.8 # it keeps increasing by 1 until it reaches
             # largest value less than 6.8
w   
```

```
## [1] 2.3 3.3 4.3 5.3 6.3
```


* Be **careful** when using something like `a:b-1` when creating a vector

```r
b <- 6
u <- 1:b - 1  # This does not create the vector 1,2,...,b-1
u
```

```
## [1] 0 1 2 3 4 5
```

```r
u <- 1:(b-1) # use this to create vector 1,2,...,b-1
u
```

```
## [1] 1 2 3 4 5
```


---

* The function **seq** is a useful function 
for creating vectors that have desired
starting and ending values.

* **seq** provides more **flexibility** than the colon operator `:`

* You can use **seq** to create a sequence with different increments than $1$

```r
seq(1, 11, by=2) # sequence that increases by 2
```

```
## [1]  1  3  5  7  9 11
```

```r
seq(1, 10, by=2) # stops at 9 since 11 is larger than 10
```

```
## [1] 1 3 5 7 9
```

```r
seq(1, 11, by=2.54) # increment by non-integer amount
```

```
## [1] 1.00 3.54 6.08 8.62
```


* Use the `length.out` argument in **seq** to 
create an equally-spaced vector with a given length.

```r
seq(1, 11, length.out=11) # same as 1:11
```

```
##  [1]  1  2  3  4  5  6  7  8  9 10 11
```

```r
seq(1, 11, length.out=6) # vector of length 6, with equal increments
```

```
## [1]  1  3  5  7  9 11
```

```r
                              # using length.out is convenient
seq(21.5, 48.2, length.out=5) # don't have to work out correct increments
```

```
## [1] 21.500 28.175 34.850 41.525 48.200
```

---

* The `rep()` (replicate) function is **very useful** for
creating vectors that have any kind of **repeated** pattern. 

* The basic form of `rep` is

```r
rep(x, times)
```
    
* **rep** produces a **vector** which repeats the vector `x` **times** number of times.
    


```r
rep(7, 3) # just creates the vector 7,7,7
```

```
## [1] 7 7 7
```

```r
rep(c(2,4,6), 3) # repeats c(2, 4, 6) three times
```

```
## [1] 2 4 6 2 4 6 2 4 6
```


* Using `rep` inside of `c()`:

```r
c(10:12, rep(c(2,4,6), 3)) 
```

```
##  [1] 10 11 12  2  4  6  2  4  6  2  4  6
```

* Using **rep** with the keyword **each** will repeat each element of `x` **each** times
  before moving on to the next element of `x`. 

```r
rep(c(2,4,6), each=4)  # repeat each element 4 times 
```

```
##  [1] 2 2 2 2 4 4 4 4 6 6 6 6
```

## Subsets of vectors

### Extracting vector elements

* You can **extract** the $k^{th}$ element of a vector by using 

```r
vector_name[k]
```

* For example:

```r
x <- c(1,3,5,100) 
x[2]  # second element of x
```

```
## [1] 3
```

```r
x[4]  # fourth element of x
```

```
## [1] 100
```


* You can also extract a **subset** of elements with indices stored by the vector `vec_index` from a vector by using

```r
vector_name[ vec_index ]
```

* For example:

```r
x <- c(1,3,5,100, 1250) 
x[ c(1,3) ]  # extract first and third elements of x
```

```
## [1] 1 5
```

```r
x[ 3:5 ]  # extract elements 3 through 5 of x
```

```
## [1]    5  100 1250
```


* You can change the value of the $k^{th}$ element of a vector
by using 

```r
vector_name[k] <- new_value
```


```r
x <- c(1,3,5,100) 
x[2] <- 6   # you may update a single element
print(x)
```

```
## [1]   1   6   5 100
```

* You can also update **multiple elements** of a vector 
by placing a vector of indices inside brackets `[]`

```r
x[1:3] <- rep(10,3) # update first 3 elements of x
print(x)
```

```
## [1]  10  10  10 100
```

### Subsetting with logical expressions

* We described above how you can take a **subset** of a vector by specifying the vector **indeces** that you want for your subset.

* You can also subset a vector using a **logical expression** rather than explicitly specifying the indeces you want.

```r
x <- c(10, 2, 21, 15)
y <- x[x > 8]  # returns all elements of x greater than 8
z <- x[x > 12] # returns all elements of x greater than 12
y
```

```
## [1] 10 21 15
```

```r
z
```

```
## [1] 21 15
```

* You can think of the expression `x[x > 8]` as doing the following:

```r
x[c(TRUE, FALSE, TRUE, TRUE)]
```

```
## [1] 10 21 15
```


### The which function

* You can find the **indeces** of a vector that satisfy a certain
condition using the **which** function.


```r
x <- c(10, 2, 21, 15)
which(x > 20) # shows that x[3] > 20
```

```
## [1] 3
```

```r
which(x > 12) # shows that x[3] > 12 and x[4] > 12
```

```
## [1] 3 4
```

* The **which** function really just returns the [**indeces**]{style="color:#D96716"} where a logical vector is `TRUE`

```r
which( c(FALSE, TRUE, FALSE) )
```

```
## [1] 2
```


## Useful methods for vectors

* The `length` function can tell you **how many** elements are in your vector:

```r
x <- 9:0
x
```

```
##  [1] 9 8 7 6 5 4 3 2 1 0
```

```r
length(x)  # length of the vector
```

```
## [1] 10
```

```r
typeof(x)  # type of elements
```

```
## [1] "integer"
```

```r
sum(x)     # sum of values
```

```
## [1] 45
```

* **R** has functions which allow you to compute 
all the well-known [**summary statistics**]{style="color:#D96716"} from a
numeric vector.


```r
x <- 1:5
mean(x)   # average of vector elements
```

```
## [1] 3
```

```r
var(x)  # variance (denominator is n-1)
```

```
## [1] 2.5
```

```r
sd(x)   # standard deviation (denominator is n-1)
```

```
## [1] 1.581139
```



```r
x <- 1:5
max(x)    # maximum value
```

```
## [1] 5
```

```r
min(x)    # minimum value
```

```
## [1] 1
```

```r
median(x) # median
```

```
## [1] 3
```


## Vectors with different data types

* As we mentioned before, **R** vectors are **not limited** to 
having numeric elements.

* The main **restriction** for **vectors** is that they must have elements which are all the **same** type.

```r
x <- c(1, 2.5, 42)  ## numeric vector
print(x)        
```

```
## [1]  1.0  2.5 42.0
```

```r
y <- c("hello","world","biostat607")  ## character vectors
print(y)
```

```
## [1] "hello"      "world"      "biostat607"
```

```r
z <- c(TRUE, FALSE, FALSE) ## logical vectors
print(z)
```

```
## [1]  TRUE FALSE FALSE
```

---

* You can "create" a vector that has **mixed data types**, but **R** will **automatically**
convert the types of some of the elements so that **all elements** have the same type.

```r
x <- c(TRUE, FALSE, FALSE) ## homogeneous logical vector
print(x)      
```

```
## [1]  TRUE FALSE FALSE
```

```r
x <- c(TRUE, FALSE, 2)  ## contains logical and numeric values
print(x)  ## R translates logical TRUE/FALSE into numeric 1/0  
```

```
## [1] 1 0 2
```

```r
x <- c(1, 2, "3")  ## numeric + character
print(x)  ## R translates numeric values translates into characters
```

```
## [1] "1" "2" "3"
```



```r
x <- c(TRUE, 2, "3") ## logical + numeric + character
print(x)  ## R translates logical and numeric values into characters
```

```
## [1] "TRUE" "2"    "3"
```


### Explicitly changing the data types

* You can convert a vector to another type using
`as.logical`, `as.numeric`, or `as.character`.


```r
x <- as.logical(c(0,1,2,3)) # numeric to logical conversion
print(x)      
```

```
## [1] FALSE  TRUE  TRUE  TRUE
```

```r
x <- as.numeric(c(TRUE,FALSE, T,F))  # logical to numeric 
print(x) 
```

```
## [1] 1 0 1 0
```

```r
x <-as.character(c(0,1,2,3)) # numeric to string
print(x)   
```

```
## [1] "0" "1" "2" "3"
```

* Sometimes conversion of a vector does **not** work


```r
## When a character cannot be converted, it returns NA 
## as an invalid number
as.numeric(c("123","12.3","123a")) 
```

```
## Warning: NAs introduced by coercion
```

```
## [1] 123.0  12.3    NA
```

```r
## Characters cannot be converted into logical values 
as.logical(c("TRUE","FALSE", "T","TF",0))  
```

```
## [1]  TRUE FALSE  TRUE    NA    NA
```

```r
as.integer(c(123, 12.3, "123", "123a"))
```

```
## Warning: NAs introduced by coercion
```

```
## [1] 123  12 123  NA
```



## Mathematical operations with vectors

* When doing **mathematical operations** with two vectors of the **same length**, **R** will perform addition, subtraction, multiplication, division **element-by-element**.


```r
x <- c(10, 5, 0)  
y <- 1:3
x+y     # element-wise addition
```

```
## [1] 11  7  3
```

```r
x*y     # element-wise multiplication
```

```
## [1] 10 10  0
```

```r
x^y     # element-wise power
```

```
## [1] 10 25  0
```


* Multiplying or dividing a vector by a **single number** multiplies (or divides) each element by that number

```r
x <- c(10, 5, 0, -5)  

3*x
```

```
## [1]  30  15   0 -15
```

```r
x/2
```

```
## [1]  5.0  2.5  0.0 -2.5
```

* Adding or subtracting a vector by a **single number** also adds (or subtracts) each element by that number

```r
x <- c(10, 5, 0, -5)  

3 + x  # Actually an example of recycling with a one-element vector
```

```
## [1] 13  8  3 -2
```

### Recycling rules

* You can actually add/subtract vectors of **different lengths** in **R**.

* When doing this, **R** **recycles** the values in the shorter vector.
    + **R** will print out a **warning** message if the length of the longer vector is **not a multiple** of the shorter vector

```r
c(1, 2, 4) + c(6, 0, 9, 10)
```

```
## Warning in c(1, 2, 4) + c(6, 0, 9, 10): longer object length is not a multiple
## of shorter object length
```

```
## [1]  7  2 13 11
```

* What the above code is doing is adding the vector `c(1, 2, 4, 1)` with the
vector `c(6, 0, 9, 10)`.

---

* Note that if we **add** a vector of **length 3** with a vector of **length 6** we will get no warning message.
    + This is because $6$ is a multiple of $3$.

```r
c(1, 2, 4) + c(6, 0, 9, 10, 11, 12)
```

```
## [1]  7  2 13 11 13 16
```

* The above code adds the vector `c(1, 2, 4, 1, 2, 4)` with the
vector `c(6, 0, 9, 10, 11, 12)`.

* I personally do not use recycling rules much when the length of 
**both vectors* is 2 or more.
    + It's probably good to be aware of recycling rules if you are getting this type of warning message.
    
    + You may find it helpful to use these recycling rules if you are, for example, adding one vector with another vector that has a simple, **repeating** pattern.

### Logical operations with vectors

* You can do **AND** and **OR**-type operations with logical vectors.
    + Remember that `&` acts like a **"vector version"** of `&&`
    + Remember that `|` acts like a **"vector version"** of `||`


```r
c(TRUE, TRUE, FALSE) & c(TRUE,FALSE,FALSE) # element-wise
```

```
## [1]  TRUE FALSE FALSE
```

```r
c(TRUE, TRUE, FALSE) | c(TRUE,FALSE,FALSE) # element-wise
```

```
## [1]  TRUE  TRUE FALSE
```

```r
c(TRUE, TRUE, FALSE) && c(TRUE,FALSE,FALSE) # only first values
```

```
## [1] TRUE
```

```r
c(TRUE, TRUE, FALSE) || c(TRUE,FALSE,FALSE) # only first values
```

```
## [1] TRUE
```



## Set operations with vectors

* You can also do **set operations** with vectors. 

* When working with **set operations**, you should think of the **set** associated with a vector as the collection of **unique** elements from that vector.

* For example, if we consider the vectors `x` and `y` defined as

```r
x <- c(1,2,3,3,4,5)   # x is c (1,2,3,3,4,5)
y <- c(1,3,3,5,7,9) # y is c (1,3,3,5,7,9) 
```
    + The **"set"** associated with `x` is $\{1,2,3,4,5\}$ and the **"set"** associated with `y` is $\{1,3,5,7,9\}$.

* Then, the **intersection** of `x` and `y` using the `intersect` function in **R** is 

```r
intersect(x,y)  # set intersection, note that repeated 3 is dropped
```

```
## [1] 1 3 5
```

* Similarly,

```r
union(x,y)     # set union
```

```
## [1] 1 2 3 4 5 7 9
```

```r
setdiff(x,y)   # set difference x - y
```

```
## [1] 2 4
```



```r
x <- 1:5            # x is c (1,2,3,4,5)
y <- c(1,3,3,5,7,9) # y is c (1,3,3,5,7,9) 
x %in% y            # membership test
```

```
## [1]  TRUE FALSE  TRUE FALSE  TRUE
```

```r
match(x, y)       # find indices of first matching values
```

```
## [1]  1 NA  2 NA  4
```

```r
setdiff(x, y)     # set difference x-y
```

```
## [1] 2 4
```


## NA and is.na(): missing values in R

* **Missing data** in R is usually represented by the 
value **NA**.
   + `NA` stands for **"Not Available"**

* You can create a vector with **NA values** by just
typing in `NA` for one of the vector elements.

```r
x <- c(1, 5, NA, 4) # The third element of this vector is NA
typeof(x)
```

```
## [1] "double"
```

* You can type in NA for either **numeric or character** variables.
     + R will automatically convert everything to the appropriate type.

```r
y <- c("cat", NA, "dog") # The second element of this vector is NA
typeof(y)
```

```
## [1] "character"
```

--- 

* Many of the **built-in** R functions will return `NA` 
if the input numeric vector **contains** any `NA` values.

* For example, if we try to compute the standard deviation of the vector `x`

```r
x <- c(1, 5, NA, 4, 7) # The third element of this vector is NA
mx <- sd(x)   # mx will have the value NA
mx
```

```
## [1] NA
```

* You can compute the **standard deviation**
of the non-NA values by including the argument `na.rm = TRUE`

```r
sx <- sd(x, na.rm=TRUE) # sx shoud have the standard deviation of 1,5,4,7
sx
```

```
## [1] 2.5
```

* In the function `sd`, the argument `na.rm` is a good example
of an argument with a **default value**.

* You can see that `na.rm` has a **default value** by looking at 
the **function definition** for `sd`

```r
sd <- function(x, na.rm = FALSE) {
    
}
```

* The **default** value of `na.rm` is `FALSE`.
    + So, you need to include `na.rm = TRUE` if you want `sd` to ignore missing values.

### The function `is.na()`

* The function `is.na()` is often very useful when you're working with data that has **mising values**.

* When applied to a vector, `is.na()` will return a vector of
**logical values** with the **same length** as the input vector.

* The $k^{th}$ element of `is.na(x)` will be `TRUE` if the $k^{th}$ element of `x` is missing.
    + Otherwise, the $k^{th}$ element of `is.na(x)` will be `FALSE`.


```r
x <- c(10, 3, 5, NA, 1, NA)  # Elements 4 and 6 of x have NA values 
is.na(x)
```

```
## [1] FALSE FALSE FALSE  TRUE FALSE  TRUE
```

* You can also use `is.na()` directly on **matrices** and **data frames**.


## Exercises

1. Suppose we define the vector `x` as `x <- 1:10`. What is the value of
`x[ seq(1, 10,by=2)][3]`?

2. Suppose `x <- rep(c(1, 5, 10), each=3)`. What is the value of `sum( x[x > 5] )`?

3. Create a vector called `xvec` that stores the following sequence of numbers:
$1, 1, 2, 1, 2, 3, 1, 2, 3, 4, ....$ and keeps repeating this pattern 
until the last number is $10$. 
   + (a) What is the length of `xvec`?
   + (b) What number is the $35^{th}$ element of `xvec`?
   + (c) What is the mean value of the numbers contained in `xvec`?
   + (d) How many elements of `xvec` equal $2$? How many elements of `xvec` equal $7$?
   + (e) What is the sum of all the **even** numbers contained in `xvec`?


