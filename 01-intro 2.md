# Getting Started {#intro}

## Using R as a calculator

* You can use R as a basic **calculator**. 

* For example, if we just type in `42 + 17` into the R console, it should print out the sum:


```r
42 + 17 
```

```
## [1] 59
```



* We can compute the square root of 243, $1.56^{124}$, and $7.21 \times 8^{4}$, just by typing these expressions into the **R console**

```r
sqrt(243)
```

```
## [1] 15.58846
```

```r
1.56*124
```

```
## [1] 193.44
```

```r
7.21*8^4
```

```
## [1] 29532.16
```

## Variables in R

* When working with more complicated mathematical operations in **R**, it is often useful to
store intermediate values in **named variables**.

* For example, the following **R** code creates the variables `x, y, z` and assigns
them the values $(42 + 17)\sqrt{43}$, $7.21(8^{4}) + \ln(2.34)$, and  
$(42 + 17)\sqrt{43}/[ 7.21(8^{4}) + \ln(2.34) ]$ respectively.


```r
x <- (42 + 17)*sqrt(43)
y <- 7.21*8^4 + log(2.34)
z <- x/y
z  ## print out the value of z
```

```
## [1] 0.01310022
```

* Here, `x`, `y`, and `z` are examples of **variables**.

* The pair of characters `<-` used together is known as the **assignment operator** in **R**.
`x <- 2` assigns the value `2` to the variable `x`.

* A **variable** is the **named storage** of a value (or an object) in memory.

* Why do we need variables?

  + To **reuse** the same value later on.
  + To **generalize** an expression to use in many cases.

* How to use variables in **R**?
  
  + To set the value of a variable, use **assignment** operator `<-`
  
  + To use the value, simply use the **variable name** as if it were its stored value.
  
* For example, ...


### Rules for choosing **variable names** in R

* Variables can be named however you want as long as you follow the 
several variable-naming rules that R has. 

* In **R** variable names can include the following:
  + **letters**: A-Z a-z
  + **digits**: 0-9
  + **underscore and period**: _ .

* Additional rules:
  + Variable names **must start with letters or a period (not underscore or digits)**
  + If a variable name starts with a **period**, it **cannot** be followed by a **number**.
  + Variable names are **case sensitive**.

* The following tables shows examples of **valid** and **invalid** variable names in R

|     Valid     |   Invalid    |
|:-------------:|:------------:|
|       i       |   2things    |
|  my_variable  |  location@   |
|   answer42    |  _user.name  |
|     .name     |     .3rd     |

* While you are free to choose variable names however you like as long as you follow the variable-naming rules of **R**, making variable names **descriptive** is highly **recommended**.

* **Descriptive** variable names make it easier to read code. This is very helpful if:
    + You are sharing your code or
    + Looking back at code you wrote many weeks/months ago

* Using a **consistent** convention for naming variables is recommended, too:

https://r4ds.had.co.nz/workflow-basics.html


### Variable Assignment

* Variables can be assigned using either `<-` or `=`


```r
x = 123    # Use = to assign a variable
y <- 123   # Or use <- to assign a variable
```


```r
x   # Retrieve the value of x
```

```
## [1] 123
```

```r
y   # Retrieve the value of y
```

```
## [1] 123
```

* The pair of characters `<-` is the classic symbol used for variable assignment in **R**.

* The use of `<-` instead of `=` is often recommended in **R** style guides:
    + http://adv-r.had.co.nz/Style.html

---

* `<-` and `=` will work the same if they are both
used in the "usual way" (when assigning variables within 
or outside of a function).

* One exception, is when used inside a **function call**. For example, if we use `=` in the function `sd(x)`:



```r
sd(x = c(1,2,3,4,5)) # only sets the argument x in sd(x) to (1,2,3,4,5)
```

```
## [1] 1.581139
```

```r
#x      ## will return an error if we try to print x
```


```r
sd(x <- c(1,2,3,4,5)) # This actually assigns the vector (1,2,3,4,5) to x
```

```
## [1] 1.581139
```

```r
x
```

```
## [1] 1 2 3 4 5
```

* However, using something like `sd(x <- c(1,2,3,4,5))` where we assign variables in a function call is not really done that often. 

* It is **not common** to assign variables in a function call (I never do it).

* Whenever, using a function `f` with a keyword such as `x`, you will generally
want to call that function using `f(x = ...)`

* So, in my opinion, there is not really a strong reason to prefer using `<-` over `=` for assignment. 

* There are other justifications for using `<-` such as the ability 
to do assignment from the left by using the reverse symbol `->`

```r
c(1, 2, 3, 4) -> a # Using c(1,2,3,4) = a will not work!  
a
```

```
## [1] 1 2 3 4
```


### Types of variables

* Variables can be used to store **different types** of values.

* Common types include numeric, text, and logical values.

```r
x <- 3.2
x
```

```
## [1] 3.2
```

* Here, `x` is actually a **vector** (basically a collection of elements storing the same type of data).

* It is a vector of **length one** (i.e., it only has one element). 

* This is the reason why you see `[1]` printed out next to the number 3.2. 
    + This means that the **first element** of the vector `x` is $3.2$. 

* **R** treats every variable as some type of collection (e.g., vectors, matrices, lists, etc.).
    + There are no separate data types in **R** for individual numbers.


* The elements in a vector can have different **types** (or modes).

* You can find the types of the elements in a vector by using the
function **typeof**

```r
y <- sqrt(1743)
typeof(y)  # double and integer are the two numeric types 
```

```
## [1] "double"
```


```r
z <- 3 # R automatically treats every number as double
z
```

```
## [1] 3
```

```r
typeof(z)
```

```
## [1] "double"
```

* The other common types for the elements in a vector include
    + **logical** (TRUE or FALSE) values
    + **character** basically text, e.g., "hello", "car", ...

```r
y <- TRUE
typeof(y)   
```

```
## [1] "logical"
```


```r
z <- "dog" # to define a character variable, place it inside quotes
typeof(z)
```

```
## [1] "character"
```

* We will discuss these types in more detail later on when
we discuss **vectors**, **matrices**, and **lists**.


## R Operations with numbers
  
* As we mentioned before, ...  


|    Operator    |       Meaning        |    Example    |    Result    |
|:--------------:|:--------------------:|:-------------:|:------------:|
|       +        |       addition       |     5 + 8     |      13      |
|       -        |     subtraction      |    90 - 10    |      80      |
|       *        |    multiplication    |     4 * 7     |      28      |
|       /        |       division       |     7 / 2     |     3.5      |
|       %%       |      remainder       |    7 %% 2     |      1       |
|       ^        |       exponent       |     3 ^ 4     |      81      |
|       **       |       exponent       |    3 ** 4     |      81      |

* R operations with numbers have similar **precedence rules** to arithmetic operations


|       Operator       |               Description               |   Precedence   |
|:--------------------:|:---------------------------------------:|:--------------:|
|         +, -         |        addition and subtraction         |      low       |
|       *, /, %%       |   multiplication, division, remainder   |      ...       |
|        **, ^         |             exponentiation              |      ...       |
|   (expressions...)   |               Parenthesis               |      high      |

* Examples of operation **precedence** can be seen when typing the following
expressions into the **R** console:


```r
1 + 2 *3 ^ 4 # power > mult/div > add/sub
```

```
## [1] 163
```

```r
(1 + 2 ) *3 ^ 4 # parenthesis > power
```

```
## [1] 243
```

## Brief intro to vectors in R

## Exercises

1. Compute the number 
```{=tex}
\begin{equation}
\frac{\sqrt{1.43 + 5^{1.2}}}{3} 
\end{equation}
```
directly in the **R** console.

2. Write an **R script** that assigns the value ...
```{=tex}
\begin{equation}
\ln\Big( 1 + \exp(-2^{1.4}) \Big) + \ln\Big(1 + 2\exp(3^{1.7}) \Big)
\end{equation}
```
to a variable named `x` and prints the result in the Console when you run
the script.

3. Which of the following is **NOT** a valid variable name in **R**?
    + .independent_variable3
    + _independent_variable3
    + independent_variable3
    + independent.variable3




