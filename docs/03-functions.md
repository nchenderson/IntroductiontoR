# Functions in R {#functions}

* A **function** in R can be thought of as a **sequence** of statements that takes some **input**, uses that input to compute something, and then returns a **result**.
  
* [**Why**]{style="color:#D96716"} do we need [**functions**]{style="color:#D96716"}?

  + To **modularize** a task so that we can reuse the same code in many places.
 
  + To increase **readability** of code.

  + To reduce **redundancy** and reduce the number of errors.


## Built-in R functions

* **base** **R** has many useful built-in functions that you can use.
   + Other **R** **packages** are another source of useful functions.

* **R's** **base** package is loaded by **default**. 
     + A few other packages including **graphics**, **stats**, and ***utils**
     are usually loaded by default as well.
 
* The **base package** includes many widely-used functions, such as the []**print()** or the **sum()** function.
 
* There are many other **R** packages available which contain many useful functions.

## Construction your own R functions

* You can write **your own** functions as needed. 

* While base R and the many available R packages have a wide range of useful functions, being able to write **your own** functions gives you much greater **flexibility** when working with **R**.

### Function Definition Syntax

* There are **three** key components of a **function definition** in R.
     + Function **name**: the name which will be used to **call** the function

     + Function **arguments**: values to pass to a function as **input**.

     + **Return** value: the value returned by a function as **output**.


* The general syntax for writing your own **R** function is:

``` r
function_name <- function(params){ 
     ## function_name is the name of the function 
     ## params name of the input variable within this function 
 
     statement1  ## statements executed when the function is called
     statement2  ## statements convert params into some value to be 
      ...        ## returned
     return(return_value)  ## return the variable return_value
}
```

### Example 1

* Let's **write a function** that takes a number as an input and returns the **square** of that number.


``` r
## define a new function named square
square <- function(x) { ## function name: square, argument : x
   return(x*x)           ## returns x*x
} 
```

* Once we have defined `square`, we can use it as many times as we would like.

* After defining the function, each time the function is used is referred to as
**calling** the function.

* Let's try **calling** `square` with an input number of `10`:

``` r
square(10)    ## example of using the function square
```

```
## [1] 100
```


### Example 2

Let's write another function that takes a single number (assumed to be an integer) as input and outputs another number according to the following rule:
    + if the input number is **positive and even**, return the number **2**
    + if the input number if **positive and odd**, return the number **1** 
    + if the input number is **not positive and even**, return the number **-2**
    + if the input number if **not positive and odd**, return the number **-1** 


``` r
PositiveEven  <- function(x) { 
   if( x > 0 & x%%2==0 ) {
       return_value <- 2
   } else if( x > 0 & x%%2==1 ){
       return_value <- 1
   } else if( x <= 0 & x%%2==0) {
       return_value <- -2
   } else {
       return_value <- -1
   }
   return( return_value )
} 
```


* Now, let's look at a few examples of **calling** `PositiveEven`:


``` r
PositiveEven(3)
```

```
## [1] 1
```

``` r
PositiveEven(-6)
```

```
## [1] -2
```

``` r
PositiveEven(0)
```

```
## [1] -2
```

``` r
PositiveEven(4)
```

```
## [1] 2
```

---

* We could make our function `PositiveEven` a bit more **user-friendly** by 
having our function throw an error whenever the 
user inputs a number that is **not** an integer.



``` r
PositiveEvenSafe <- function(x) { # Function named PositiveEvenSafe
   if( x%%1 != 0) { # x%%1 will equal 0 if x is an integer 
       stop("x must be an integer")  
       # The stop function will stop the execution 
       # of the function and will return an error
       
   }
   if( x > 0 & x%%2==0 ) {
       return_value <- 2
   } else if( x > 0 & x%%2==1 ){
       return_value <- 1
   } else if( x <= 0 & x%%2==0) {
       return_value <- -2
   } else {
       return_value <- -1
   }
   return( return_value )
} 
```

* Now, let's see what happens if we call the function `PositiveEvenSafe` with 
the argument `x = 2` and then `x = 7.1`

``` r
PositiveEvenSafe(2)
```

```
## [1] 2
```


``` r
PositiveEvenSafe(7.1)
Error in PositiveEvenSafe(7.1) : x must be an integer
```

### Rules for choosing function names

* All the same **rules** for **variable names** apply to
rules for choosing **function names**.

* Examples of valid and invalid function names include:


|  Valid_Function_Names  |  Invalid_Function_Names  |
|:----------------------:|:------------------------:|
|           i            |         2things          |
|      my_function       |        location@         |
|        answer42        |        _user.name        |
|         .name          |           .3rd           |

---

* Another rule to keep in mind is that you cannot use a  **reserved word** 
as a function name or variable name.

* You **can** use built-in function names (for example, the **print** function) for your own functions, but this is **NOT RECOMMENDED**.

* The following are the **reserved words** in R:

**if else while function for**

**in next break TRUE FALSE**

**NULL Inf NA NA_integer**

**NA_real NA_complex NA_character**

* You can find the list of **reserved words** in **R** by typing 

``` r
?reserved
```
directly in the R console

## Default argument values in functions

* We can provide **default values** for function parameters/arguments
    + by adding **= default_value** after the parameter

* If an argument is **specified** in the function call, the specified one is used

  + Otherwise; the **default** argument value is used

* In the function definition, it is generally better (though not required) to put parameters **without default arguments** **before** those with **default arguments**. 
   + When **calling** a function, arguments must be specified for **every parameter** without default arguments.

   + Unlike **Python**, in **R** you can mix arguments with/without default arguments in an arbitrary order (though I don't recommend it).


### Example 1

* As an example, let's write a function that adds 3 numbers and, **as a default**, 
sets one of these numbers to zero:

``` r
add3 <- function(x, y, z=0) {
    return(x + y + z)
}
```

* The **default** value for `z` here is $0$.
  

``` r
add3(1, 2)     ## omit z
```

```
## [1] 3
```

``` r
add3(1, 2, 0)  ## this should give the same as add3(1,2)
```

```
## [1] 3
```

``` r
add3(1, 2, 3)  ## set z to 3 instead of 0
```

```
## [1] 6
```
  

##  Specifying function arguments with keywords

* We can specify how arguments are passed to parameters not only by their
order but by **names** with **keyword arguments**.

* **Keyword arguments**: have to do with how you **call** a function - not with the function definition itself.

* For example, we could call our function `add3` with  **keywords** in the following way:

``` r
add3(2, 2, 1)      # Call function using original positions
```

```
## [1] 5
```

``` r
add3(x=2, y=2, z=1) # Call function using keywords
```

```
## [1] 5
```

``` r
add3(y=2, x=2, z=1) # With keywords, position does not matter
```

```
## [1] 5
```


### Example 1

* The function `foo` below has parameters `x`, `y,`, `z`, `w`.
    + The **default** value of `z` is $0$, and the **default** value of `w` is **TRUE**.


``` r
foo <- function (x, y, z=0, w=TRUE) { 
    if(w) {
       1000*x + 100*y + 10*z  ## this is equivalent to return(...)
    } else {
       1000*x - 100*y + 10*z
    }
} 
```

* Let's try **calling** `foo` using the **original position** of the 
arguments in the function definition.


``` r
foo(9, 3, 5,TRUE) ## specify all arguments
```

```
## [1] 9350
```

``` r
foo(9, 3, 5)      ## omit argument w
```

```
## [1] 9350
```

``` r
foo(9, 3)       ## omit both z and w
```

```
## [1] 9300
```


* Now, let's try calling `foo` using **keyword** arguments and 
change the orders of `x` and `y`.

``` r
## foo(9)      ## this will cause error because y is unknown
foo(x=9, y=5)   ## specify x and y as keyword arguments
```

```
## [1] 9500
```

* We can even switch the positions of `x` and `y` when using **keyword**
arguments

``` r
foo(y=5, x=9)  ## when using keywords, argument order doesn't matter
```

```
## [1] 9500
```

* You can even **mix** which arguments you specify as positional and keyword:

``` r
foo(9, y=5)     ## specify x as positional, y as keyword argument
```

```
## [1] 9500
```

``` r
foo(9, z=3, y=5)  ## y,z are keyword arguments, x is positional
```

```
## [1] 9530
```

## More Examples of Writing Functions


### Example 1: Pass/Fail from a Weighted Average

* Let's write an **R** function called `WeightedGrade` that computes a weighted average of a collection of test scores
and outputs whether or not a student has "passed" or "failed" the course - using two possible criteria for choosing Pass/Fail. 

* We would like the R function to have the following structure

``` r
WeightedGrade <- function(grades, weights, scheme="A") { 
   
}
```


* **Function Input:** We want the inputs `grades` and `weights` to be both numeric vectors of the same length.
    
    - From `grades` and `weights` the **weighted grade average**, is the sum of elements in
`grades` multiplied by the elements in `weights` divided by the sum of `weights`. 

    - All the elements of both `grades` and `weights` should be greater than or equal to $0$ and less than or equal to $100$.

---

* **Function Output**: If the sum of `weights` equals $100$ and `scheme=="A"`, the function should return 
a character vector using the following rule: 
    + `"Pass"` if the weighted grade average using `grades` and `weights` is greater than $60$
and return `"Fail"` if the weighted grade average is less than or equal to $60$.

* If the sum of `weights` equals $100$ and `scheme=="B"`, the function should return
a character vector using the following rule:
    +  `"Pass"` if the weighted grade average using `grades` and `weights` is greater than $80$
and return `"Fail"` if the weighted grade average is less than or equal to $80$.

* If the sum of `weights` does not equal $100$, the function should return the value `NA`.

---

* Here is one way to write the function so that it satisfies the above description: 

``` r
WeightedGrade <- function(grades, weights, scheme="A") {
    if(sum(weights) != 100) {
        ## if sum(weights)!=100, return NA
        ans <- NA
    } else if(scheme=="A") {
        ## if sum(weights)==100 and scheme is A, use the 
        ## following Pass/Fail rule
        weighted_avg <- sum(weights*grades)/sum(weights)
        if(weighted_avg > 60) {
            ans <- "Pass"
        } else {
            ans <- "Fail"
        }
    } else {
        ## if sum(weights)==100 and scheme is not A, use the 
        ## following Pass/Fail rule
        weighted_avg <- sum(weights*grades)/sum(weights)
        if(weighted_avg > 80) {
           ans <- "Pass"
        } else {
           ans <- "Fail"
        }
    }
    return(ans)
}
```

---

* Now, let's test out our function by doing a few example runs:

``` r
WeightedGrade(grades=c(60, 75, 80), weights=c(10, 40, 50), scheme="B")
```

```
## [1] "Fail"
```

``` r
WeightedGrade(grades=c(60, 75, 80), weights=c(10, 40, 50), scheme="A")
```

```
## [1] "Pass"
```

``` r
## Note that scheme is a default argument
WeightedGrade(grades=c(60, 75, 80), weights=c(10, 40, 50) ) 
```

```
## [1] "Pass"
```

``` r
WeightedGrade(grades=c(60, 75, 80), weights=c(10, 30, 40) )
```

```
## [1] NA
```

``` r
WeightedGrade(grades=c(90, 95, 80, 86), weights=c(10, 10, 40, 40), scheme="B" )
```

```
## [1] "Pass"
```


### Example 2: ...

* Let's write an **R** function called `RepSumLT` that computes the proportion where two vectors with a certain
repeating are less than a user-supplied cutoff value.

* We would like the `RepSumLT` function to have the following structure

``` r
RepSumLT <- function(x, m, tau=0) { 
   
}
```


* **Function Input:** We want the argument `x` in `RepSumLT` to be a vector.

    - Both `m` and `tau` should be vectors of length $1$. The only element of `m` should be a positive integer.


* **Function Output:** The function should return the **proportion** of indices where both elements of the vectors `rep(x, times=m)`
and `rep(x, each=m)` are less than or equal to `tau`.



* As an example, the function call 
`RepSumLT(x=c(1,2), m=2, tau=1)` should return the value $0.25$ because 
`c(1, 2, 1, 2)` and `c(1, 1, 2, 2)` are vectors of length 4 and are only both less than or equal to $1$ 
at vector index $1$.

* Here is one way to write the function so that it satisfies the above description: 

``` r
RepSumLT <- function(x, m, tau=0) {
    y <- rep(x, times=m)
    z <- rep(x, each=m)
    ans <- mean((y <= tau)*(z <= tau))
    return(ans)
}
```

* Let's try running `RepSumLT` on a few examples:

``` r
RepSumLT(x=1:10, m=3, tau=3)
RepSumLT(x=-10:10, m=3)
RepSumLT(x=seq(0.2, 5.2, by=0.45), m=4, tau=3.0)
RepSumLT(x=seq(-3.2, 5.2, by=0.45), m=4)
```



## Exercises

1. Suppose we define the function `quiz` as

``` r
quiz <- function(bool_var1, x=0, bool_var2 = TRUE) {
    y <- 0
    if(bool_var1 & bool_var2) {
        y <- x + 2
    } else {
        if(bool_var1) {
            y <- x - 2
        }
    }
    return(y)
}
```
What value does the following function call return?

``` r
quiz(FALSE, 1.3)
```


2. Write an **R function** that implements the following
mathematical function in **R**
```{=tex}
\begin{equation}
L(x, y) = 
\begin{cases}
0 & \text{ if } x = 0 \text{ and } y = 0 \nonumber \\
1 & \text{ if } x \neq 0 \text{ and } y = 0 \nonumber \\
|x| & \text{ if } y = 1 \nonumber \\
x^{2} & \text{ if } y = 2 \nonumber 
\end{cases}
\end{equation}
```
The function should have user-provided arguments `x` and `y`
and should return `NA` if `y` does not equal either $0$, $1$, or $2$


3. Write an **R** function called `PropGtZero` which returns the proportion
of three entered numbers which are greater than $0$.
 The function should have the following **function definition**

``` r
PropGtZero <- function(x, y, z, gt=TRUE) {
  
}
```
   + If `gt=TRUE`, then `PropGtZero` should return the  proportion of the numbers `x`, `y`, `z` which are greater than $0$.
   + If `gt=FALSE`, then `PropGtZero` should return the 
proportion of the  numbers `x`, `y`, `z` which are lesser than or equal to $0$.
   + If one or more of `x`, `y`, `z`, is `NA`, the function should return `NA`.

* For example, `PropGtZero(3,2,-2)` should return $2/3$.


