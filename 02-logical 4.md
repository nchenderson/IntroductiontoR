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

