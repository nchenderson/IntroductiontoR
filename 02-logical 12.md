# (PART) R Programming Fundamentals {-}

# Logical Expressions and If-Else Statements in R {#ifelse}



## Logical Expression in R

* A **Logical** expression is an expression that evaluates to either **TRUE** or **FALSE**.

* The following are examples of logical expressions in **R**:
    + `4 > 2`
    + `3 <= 5`
    + `15.0 + 1.3*1.3 > 17.0`
    + ` "cat" == "dog" `
    
* Each of the above expressions will evaluate to either
**TRUE** or **FALSE** if you run them in R.


```r
4 > 2
```

```
## [1] TRUE
```


```r
3 <= 5
```

```
## [1] TRUE
```


```r
15.0 + 1.3*1.3 > 17.0
```

```
## [1] FALSE
```


```r
x <- "cat" == "dog" # assign to the variable x the value 
                    # returned by this logical expression
x
```

```
## [1] FALSE
```

---

* Most logical expressions are constructed by using some **combination** of:
    + **Comparison** operators (<, <=, ==, !=)
    + **Logical** operators (**and**, **or**, **not**) (in **R**: &&, ||, !)

### Comparison Operators


|    Operator    |            Meaning             |       Example        |    Result    |
|:--------------:|:------------------------------:|:--------------------:|:------------:|
|       <        |           Less than            |        5 < 3         |    FALSE     |
|       >        |          Greater than          |        5 > 3         |     TRUE     |
|       <=       |     Less than or equal to      |        3 <= 6        |     TRUE     |
|       >=       |    Greater than or equal to    |        4 >= 3        |     TRUE     |
|       ==       |            Equal to            |        2 == 2        |     TRUE     |
|       !=       |          Not equal to          |    'str' != 'stR'    |     TRUE     |

### Logical Operators

* The first main logical operator we will discuss is the **logical AND**

* In **R**, the logical operator **&&** is used to represent the logical **AND**

* The **logical AND** is used to test whether or not two statements are **both** true.

* For two logical expressions **A** and **B**, the logical expression **A && B** is true
only if both **A** and **B** evaluate to true.


```r
4 > 2 && 5/2 == 1   ## only the first statement is TRUE
```

```
## [1] FALSE
```

```r
4 > 2 && "car" == "truck"   ## only the first statement is TRUE
```

```
## [1] FALSE
```

```r
4 > 2 && 3 < 5   ## both statements are TRUE
```

```
## [1] TRUE
```

---


* The logical operator **||** is used in **R** to represent the logical **OR**.

* For two Boolean expressions **A** and **B**, the Boolean expression **A || B** is true if at least one of **A** and **B** evaluates to true.

* Note that if **A** and **B** are both true, **A || B** will be true; **or** does not mean only one of
**A** and **B** is true.


```r
4 > 2 || 5/2 == 1  ## only the first statement is TRUE
```

```
## [1] TRUE
```

```r
4 > 2 || "car" == "truck"  ## only the first statement is TRUE
```

```
## [1] TRUE
```

```r
4 > 2 || 3 < 5  ## both statements are TRUE
```

```
## [1] TRUE
```


---

* The logical operator **!** is used to represent the logical **NOT**.

* If the logical expression **A** is true, then **! A** is false.


```r
!4 > 2  
```

```
## [1] FALSE
```

```r
!4 > 2 && 3 > 1  ## !4 > 2 is FALSE
```

```
## [1] FALSE
```

```r
!(!4 > 2 && !3 > 1) ## expression in parentheses is evaluated first
```

```
## [1] TRUE
```

---

* Note that we can apply logical operations to the keywords `TRUE` and `FALSE` themselves:

```r
TRUE && FALSE ## logical AND
```

```
## [1] FALSE
```

```r
TRUE || FALSE ## logical OR
```

```
## [1] TRUE
```

```r
!TRUE  ## logical NOT
```

```
## [1] FALSE
```

* The below table summarizes the logical operations discussed.
  

|      Operator      |      Meaning      |            Example             |    Result    |
|:------------------:|:-----------------:|:------------------------------:|:------------:|
|         !          |    Logical NOT    |             !TRUE              |    FALSE     |
|                    |                   |             !FALSE             |     TRUE     |
|         &&         |    Logical AND    |         FALSE && FALSE         |    FALSE     |
|                    |                   |         TRUE && FALSE          |    FALSE     |
|                    |                   |         FALSE && TRUE          |    FALSE     |
|                    |                   |          TRUE && TRUE          |     TRUE     |
|    &#124;&#124;    |    Logical OR     |    FALSE &#124;&#124; FALSE    |    FALSE     |
|                    |                   |    TRUE &#124;&#124; FALSE     |     TRUE     |
|                    |                   |    FALSE &#124;&#124; TRUE     |     TRUE     |
|                    |                   |     TRUE &#124;&#124; TRUE     |     TRUE     |

### Precedence with logical operations


|        Operators        |                 Meaning                 |   Precedence   |
|:-----------------------:|:---------------------------------------:|:--------------:|
|   &&, &#124;&#124;, !   |            Boolean operators            |      Low       |
|          +, -           |        Addition and subtraction         |                |
|        *, /, %%         |   Multiplication, division, remainder   |                |
|          **, ^          |             Exponentiation              |                |
|    (expressions ...)    |               Parenthesis               |      High      |

* Mathematical operations are generally performed before logical operations.

```r
4 + 2 > 5
```

```
## [1] TRUE
```

```r
4 + 2 == 6
```

```
## [1] TRUE
```






### Abbreviating TRUE and FALSE with T and F

* You can use `T` and `F` in place of `TRUE` and `FALSE` 
    + I usually **do not** use `T` and `F`, but you will often see `T` and `F` used.

```r
T     ## T is shorthand for TRUE
```

```
## [1] TRUE
```

```r
F     ## F is shorthand for FALSE
```

```
## [1] FALSE
```

```r
T && F
```

```
## [1] FALSE
```

```r
T || F
```

```
## [1] TRUE
```


* While you can use `T` and `F` in place of `TRUE` and `FALSE`, it is good practice to be **careful** when using these logical **abbreviations**.


```r
T <- 2   ## T is defined as a variable

          ## Now T represents a vector with 
T         ## a number value, not TRUE
```

```
## [1] 2
```

```r
F        ## F still represents FALSE
```

```
## [1] FALSE
```

```r
## FALSE <- 3   # this will result in an error

## TRUE and FALSE cannot be redefined, thus safer to use
```


### Examples of logical operations in R


```r
TRUE || FALSE  ## boolean OR
```

```
## [1] TRUE
```

```r
!TRUE          ## NOT operator
```

```
## [1] FALSE
```

```r
!TRUE || TRUE    ## Which one will get evaluated first?
```

```
## [1] TRUE
```

```r
! (TRUE || TRUE) ## How about this time?
```

```
## [1] FALSE
```


### && vs. & and || vs. |

* You can also use `&` for the logical **AND** operator.

* You can also use `|` for the logical **OR** operator.
    
* When comparing logical vectors of **length 1**:
   + && and & will return the **same thing**. 
   + || and  | will return the **same thing**.
   
* && vs. & or || vs. | only differ when comparing **logical vectors** that have lengths **longer than 1**.


```r
TRUE & FALSE  ## Same as TRUE && FALSE
```

```
## [1] FALSE
```

```r
TRUE | FALSE  ## Same as TRUE || FALSE
```

```
## [1] TRUE
```


* As an example of the distinction between && and &, let us define two logical vectors `x` and `y`

```r
x <- c(TRUE, FALSE, TRUE, FALSE)
y <- c(TRUE, TRUE, FALSE, FALSE)
x
```

```
## [1]  TRUE FALSE  TRUE FALSE
```

```r
y
```

```
## [1]  TRUE  TRUE FALSE FALSE
```

* Let's see what happens if we then run `x && y` and `x & y`:


```r
x && y  ## && just compares the first two elements 
```

```
## [1] TRUE
```

```r
x & y  ## & returns a vector comparing element-by-element
```

```
## [1]  TRUE FALSE FALSE FALSE
```

* Similarly, let's see what happens when we run `x || y` vs. `x | y`:

```r
x || y  ## || just compares the first two elements 
```

```
## [1] TRUE
```

```r
x | y  ## | returns a vector comparing element-by-element
```

```
## [1]  TRUE  TRUE  TRUE FALSE
```

```r
!x
```

```
## [1] FALSE  TRUE FALSE  TRUE
```

## If and If-else statements 


### if statements

* In **R**, the form of an [**if statement**]{style="color:#D96716"} is the following:

```r
if( condition ) {
    code_chunk1
}
```

* `condition` is usually a **logical expression**, but could just be a logical vector of length 1 (i.e., TRUE or FALSE). 

* If `condition` evaluates to **TRUE**, `code_chunk1` will be executed.

* You actually do not have to **indent** the code in `code_chunk1`, but I would **recommend** that you do indent.


* The code inside {...} will be executed 
only if the **condition** of the **if statement** is TRUE.


```r
if (TRUE) { # if condition is TRUE 
  "hello"   # this statement will run
}
```

```
## [1] "hello"
```

```r
if (FALSE) { # if condition is FALSE 
  "world"   # this statement will NOT run
}
```


### if statement examples


```r
x <- 1
y <- 2
if (x < y ) {
  "x is smaller than y"
}
```

```
## [1] "x is smaller than y"
```

```r
if (x > y ) {
  "x is greater than y"
}
```




```r
x <- 3
y <- 2
if (x < y ) {
  "x is smaller than y"
}

if (x > y ) {
  "x is greater than y"
}
```

```
## [1] "x is greater than y"
```




```r
if( 2 < 3 ) {
    "Hello"
}
```

```
## [1] "Hello"
```


```r
if( "dog" == "cat" ) {
    "Hello"
}
```


```r
d = 2
if( d < 3 && d == 2.5) {
    "Hello"
}
```


```r
if( 2 < 3 || 2 == 2.5) {
    "Hello"
}
```

```
## [1] "Hello"
```


### Single-line if statements

* If the code to be executed in the if statement is short, 
you can write it immediately after `if(condition)` on the **same line**.

* Or, you can write the single-line statement on the line immediately below `if(condition)`


```r
x = 5
if(x > 4 & TRUE) x = 2*x # multiply x by 2
x
```

```
## [1] 10
```

* This **single-line** if statement is the same as using:

```r
x = 5
if(x > 4 & TRUE) { 
    x = 2*x # multiply x by 2
}
x
```

```
## [1] 10
```


## if-else statements

* In many cases, you want to perform **an action** if a condition is true but perform **another action** if that condition is false.

* This can be done with an **if-else** statement.
* In **R**, the form of an **if-else** statement is the following:

```r
if( condition ) {
    code_chunk1
} else {
    code_chunk2
}
```

* As with if statements, `condition` is usually a logical expression, but could just be a logical vector (with a single element). 

* If `condition` evaluates to **TRUE**, `code_chunk1` will be executed.
    
* Otherwise, if condition evaluates to **FALSE**, `code_chunk2` will be executed.

---

* As an example, let's write an if-else statement that computes the **absolute value** of a number.


```r
x <- -3.2
if( x > 0 ) {
   abs_x <- x   # assign the variable abs_x the 
                # value stored in x
} else {
   abs_x <- -x   # assign the variable abs_x the 
                 # negative of the value stored in x
}
abs_x   # print the value stored in abs_x
```

```
## [1] 3.2
```

* Another if-else example:


```r
x <- 5
if( x%%2 == 0 ) { # arithmetic operation x%%2 evaluated first
   "Hello"
} else {
   "world"
}
```

```
## [1] "world"
```

* Another if-else example:


```r
x <- 5
if( x%%2 == 0 | x > 4) {
   "Hello"
} else {
   "world"
}
```

```
## [1] "Hello"
```


### if-else-if chains

* In many cases, a desired computation will depend on **more**
than 2 conditions.

* For these cases, you can use an **if - else if - else** chain of conditional statements.

* The general syntax for an **if - else if - else** chain in **R** is:

```r
if ( condition1 ) {  ## If condition1 is TRUE,
    code_chunk1     ##  code_chunk1 will be executed.
} else if ( condition2 ) { ## If condition1 is FALSE
                           ## and condiiton2 is TRUE,
    code_chunk2          ## code_chunk2 will be executed
} else if ( condition3 ) { ## If both conditions 1 and 2 are FALSE
                           ## and condition3 is TRUE,
   code_chunk3             ## code_chunk3 will be executed
}
.
.
} else {      ## If all previous conditions are FALSE,
   else_chunk  ##  else_chunk will be executed
}
```


* An if-else if-else example:


```r
x = 2
if ( x < 0 ) {        ## If the condition is TRUE,
  "x is negative"     ## this statement will run.
} else if ( x == 0 ) {## If previous conditions are FALSE but this
  "x is zero"         ## is TRUE, this statement will run.
} else {              ## If previous conditions are FALSE,
  "x is positive"     ## this statement will run.
}
```

```
## [1] "x is positive"
```


* Another if-else if-else example:


```r
message <- "second"
if ( message == "first" ) {   
    "hello"
} else if ( message == "second" ) {
    "world"
} else {
    "nothing"
}
```

```
## [1] "world"
```

---

* Be careful about the **location** of **else** in if-else if-else statements

* In **R**, you do not want to start a line with **else if** or **else**.


### Nested if-else statements 

* You can certainly have if-else statements **within**
a conditional statement.


```r
x = 3
if ( x %% 2 == 0 ) {  ## first condition
  if ( x < 0) {       ## second condition 
    "x is even and negative"
  } else {
    "x is even and non-negative"
  } 
}  else if ( x < 0 ) {## this if statement is not nested
  "x is odd and negative"         
} else {              ## not nested either
  "x is odd and non-negative"     
}
```

```
## [1] "x is odd and non-negative"
```


## Exercises

1. What will be printed to the screen if you run the **R** code below?

```r
x <- 2
if(3 < 2 || TRUE) {
    x <- 2*x
} else {
    x <- 0
}
print(x)
```




