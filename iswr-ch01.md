---
title: "Introductory Statistics with R - Chapter 1"
author: "Arthur Ryman"
date: "January 22, 2016"
output: slidy_presentation
---

## CKME 132 Data Analytics: Basic Methods

### Introductory Statistics with R
### Chapter 1: Basics

<img src="http://ryersonu-datasciencelab.github.io/courses/images/chang-school-logo.png" style="width:2in" />

## Introduction

- this presentation is based on _Introductory Statistics with R_, _Chapter 1: Basics_
- this is an R Markdown presentation
    - Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents
    - R Markdown let's you combine R input and output, including graphs, with text
    - for more details on using R Markdown see <http://rmarkdown.rstudio.com>.

## 1 Basics

- this chapter gets you started with R
- for best results, install R and RStudio on your personal computer
    - download R from <https://www.r-project.org> and install it
    - download RStudio from <https://www.rstudio.com> and install it
    - launch the RStudio application to verify the installation

## The R Project for Statisical Computing

<img src="images/r-resources/www-r-project-org.tiff" style="width:8in" />

## RStudio

<img src="images/r-resources/www-rstudio-com.tiff" style="width:8in" />

## 1.1 First Steps

- this section introduces you to the R computing environment
- you'll mainly use RStudio in this course

## RStudio Startup

<img src="images/r-resources/rstudio-startup.tiff" style="width:8in" />

## The ISwR Package

- the ISwR package contains data sets used in the book
- install the ISwR package on your computer
    - do this once


```r
install.packages("ISwR")
```

- load the ISwR library into your R session
    - do this when you start a new session


```r
library(ISwR)
```

## Your first plot

- try this


```r
plot(rnorm(1000))
```

<img src="iswr-ch02_files/figure-slidy/unnamed-chunk-68-1.png" title="" alt="" width="768" />

- R generated and plotted a **vector** of 1000 numbers randomly **sampled** from the **normal distribution**
- notice how the dots are more **dense** at height 0 and thin out away from 0

## 1.1.1 An overgrown calculator

- R can perform arithmetic using the usual operators


```r
2+2
```

```
## [1] 4
```


```r
4*(5+6)
```

```
## [1] 44
```

- R has a large set of mathematical functions, e.g. the **exponential** function `exp(x)` = $e^x$


```r
exp(-2)
```

```
## [1] 0.1353353
```

- R can operate on single numbers, vectors, and higher-dimensional arrays of numbers
- the output includes labels to help you locate each number
    - e.g. [6] means the row begins with the sixth number


```r
rnorm(15)
```

```
##  [1]  0.62038548  1.65997650  0.25188221 -0.98343836 -0.31344553
##  [6] -0.83777898  0.46315614 -0.06717987  0.14499172  0.58662531
## [11]  1.61646908 -0.12393794  0.83632798  3.19445771  2.41117911
```

## 1.1.2 Assignments

- R let's you assign values to symbolic variables
    - variable names may contain letters, digits, underscore (_), and dot (.) with some restrictions
    - names that start with dot are used for system variables
- assign the value `2` to the variable `x`

```r
x <- 2
```

- print the value of `x`

```r
x
```

```
## [1] 2
```

- you then can use the variable in other expressions
- use `x` in an expression

```r
x + x
```

```
## [1] 4
```

- R variables can be freely reassigned new values of any type
    - unlike strongly typed languages such as Java or C#
- assign the character string `"Hello"` to `x`

```r
x <- "Hello"
```

- avoid using variables that are already used by R
    - some single-letter variable names to avoid: `c, q, t, C, D, F, I, T`

## 1.1.3 Vectorized arithmetic

- statistical calculations involve sequences of values
    - e.g. measurements of height: $x_1, x_2, \ldots , x_n$
- these are referred to as **vectors**
- you can construct vectors using the **concatenate** function `c(...)`

```r
weight <- c(60,72,57,90,95,72)
weight
```

```
## [1] 60 72 57 90 95 72
```

- R has many other ways to create vectors
    - generate sequences
    - randomly sample distributions
    - read data from files, databases, the web
    
- R has built-in vector operations
    - no need to write programmatic loops like in most other computer languages

- given weight $w$ in kilograms and height $h$ in metres compute the Body Mass Index $\mathrm{BMI}$

$$\mathrm{BMI} = \frac{w}{h^2}$$


```r
height <- c(1.75, 1.80, 1.65, 1.90, 1.74, 1.91)
bmi <- weight / height^2
bmi
```

```
## [1] 19.59184 22.22222 20.93664 24.93075 31.37799 19.73630
```

- given a vector $x$ of $n$ observations, compute its 
    - **mean** $\bar{x}$ and 
    - **standard deviation** $\mathrm{SD}$
    
$$
\bar{x} = \frac{\sum_{i=1}^n x_i}{n}
$$


```r
sum(weight)
```

```
## [1] 446
```

```r
sum(weight) / length(weight)
```

```
## [1] 74.33333
```

$$
\mathrm{SD} = \sqrt{\frac{\sum_{i=1}^n (x_i - \bar{x})^2}{n - 1}}
$$


```r
xbar <- sum(weight)/length(weight)
weight - xbar
```

```
## [1] -14.333333  -2.333333 -17.333333  15.666667  20.666667  -2.333333
```

- R recycled the variable `xbar` to match the length of the vector `weight`


```r
(weight - xbar)^2
```

```
## [1] 205.444444   5.444444 300.444444 245.444444 427.111111   5.444444
```

- now sum the squares

```r
sum((weight - xbar)^2)
```

```
## [1] 1189.333
```

- combine these expressions

```r
sqrt(sum((weight - xbar)^2)/(length(weight)-1))
```

```
## [1] 15.42293
```

- R has built-in functions for mean and standard deviation

```r
mean(weight)
```

```
## [1] 74.33333
```

```r
sd(weight)
```

```
## [1] 15.42293
```

## 1.1.4 Standard procedures

- R has many built-in statistical procedures
- you'll learn the theory behind tests of statistical significance later in this course
- here you'll apply a built-in test to the BMI data
- normal BMI ranges from 20 to 25
- therefore the mean BMI is 22.5
- you can test our BMI data against this mean using the t-test


```r
t.test(bmi, mu=22.5)
```

```
## 
## 	One Sample t-test
## 
## data:  bmi
## t = 0.34488, df = 5, p-value = 0.7442
## alternative hypothesis: true mean is not equal to 22.5
## 95 percent confidence interval:
##  18.41734 27.84791
## sample estimates:
## mean of x 
##  23.13262
```

- the large p-value tells us that it is very probable that our BMI data did come from a population whose mean is 22.5

## 1.1.5 Graphics

- graphical visualisation of data is often the first step in analysis
- R provides many standard statistical graphs
- consider the relation between weight and height in our BMI data

```r
plot(height, weight)
```

<img src="iswr-ch02_files/figure-slidy/unnamed-chunk-88-1.png" title="" alt="" width="768" />

- R gives you a lot of control over the appearance of graphs
- let's change the **plot character** `pch`

```r
plot(height, weight, pch=2)
```

<img src="iswr-ch02_files/figure-slidy/unnamed-chunk-89-1.png" title="" alt="" width="768" />

- if the average BMI is 22.5 then the relation between weight and height is approximately $w = 22.5 h^2$
- let's add a curve that shows this relation to the plot
    - define a vector `hh` of regularly spaces height values at which to compute the expected weight
    - connect the computed points by line segments


```r
plot(height, weight, pch=2)
hh <- c(1.65, 1.70, 1.75, 1.80, 1.85, 1.90)
lines(hh, 22.5 * hh^2)
```

<img src="iswr-ch02_files/figure-slidy/unnamed-chunk-90-1.png" title="" alt="" width="768" />

## 1.2 R language essentials

- this section outlines basic concepts
- the focus is on language elements that are useful for interactive use

## 1.2.1 Expressions and objects

- R provides a **Read-Evaluate-Print-Loop** (REPL) mode of interaction
- all R expressions produce a, possibly `NULL` result
    - may be invisible
- some expressions have **side effects**
    - open a graphics window
    - write a file
- expressions work on **objects**
    - anything that can be assigned to a variable
    - vectors, arrays, lists, data frames, ...

## 1.2.2 Functions and arguments

- many R expressions involve the use of **function calls**
    - e.g. `plot(height, weight, pch=2)`
    - a **function name**, e.g `plot`
    - followed by parentheses enclosing a list of zero or more **actual arguments**, e.g. `(height, weight, pch=2)`
    - some arguments are **positional**, e.g. `height` and `weight`
    - some arguments are **named**, e.g. `pch=2`
- a function is defined in terms of **formal arguments**
    - e.g. `plot <- function(x,y,...)`
    - positional actual arguments are matched to formal arguments by **positional matching**
    - named actual arguments are matched to formal named arguments by **keyword matching**
    - a formal argument may have a **default value** which is used if no actual argument matches it
- you can mix positional and named actual arguments in a function call
    - named arguments may appear in any order
    - e.g. `plot(y=weight, x=height)`
- print the formal arguments of a function

```r
args(plot.default)
```

```
## function (x, y = NULL, type = "p", xlim = NULL, ylim = NULL, 
##     log = "", main = NULL, sub = NULL, xlab = NULL, ylab = NULL, 
##     ann = par("ann"), axes = TRUE, frame.plot = axes, panel.first = NULL, 
##     panel.last = NULL, asp = NA, ...) 
## NULL
```
- notice how default values are specified

## 1.2.3 Vectors
- R supports **numeric**, **character**, and **logical** vectors
    - we've been dealing with numeric vectors in the BMI data
    - all vectors may also contain the special value `NA` to indicate missing data
    
- a character vector contains text strings


```r
c("Huey","Dewey","Louie")
```

```
## [1] "Huey"  "Dewey" "Louie"
```

- you can use single or double quotes


```r
c('Huey','Dewey','Louie')
```

```
## [1] "Huey"  "Dewey" "Louie"
```

- a logical vector contains `TRUE` and `FALSE` values
    - R defines abbreviations `T` and `F`


```r
c(T,T,F,T)
```

```
## [1]  TRUE  TRUE FALSE  TRUE
```

- logical vectors typically arise when you are expressing conditions on data using **relational operators**


```r
bmi > 25
```

```
## [1] FALSE FALSE FALSE FALSE  TRUE FALSE
```

## 1.2.4 Quoting and escape sequences

- the value of a text string does not include the enclosing quotes you used to enter it
- the **catenate** function `cat()` prints the character contents of strings


```r
cat(c("Huey", "Dewey", "Louie"))
```

```
## Huey Dewey Louie
```

- sometimes you may need to include quotes in the text string or include non-printable characters such as the
newline
- this is accomplished using **escape** sequences that begin with the backslash character (\\)


```r
cat("What\nis\n\"R\"?")
```

```
## What
## is
## "R"?
```

## 1.2.5 Missing values

- real-world data often is incomplete
- R has a special value `NA` to indicate that a data value is missing, i.e. **Not Available**
- `NA` acts like an ordinary value in many respects except that operations that involve `NA` produce `NA`


```r
c(1,2,3)+c(4,5,NA)
```

```
## [1]  5  7 NA
```

- you can test for `NA` values

```r
is.na(c(4,5,NA))
```

```
## [1] FALSE FALSE  TRUE
```

## 1.2.6 Functions that create vectors

- the functions `c`, `seq`, and `rep` produce vectors

- you've already seen the **concatenate** function `c()`


```r
c(42,57,12,39,1,3,4)
```

```
## [1] 42 57 12 39  1  3  4
```

- you can concatenate two or more vectors or values


```r
x <- c(1,2,3)
y <- c(10,20)
c(x,y,5)
```

```
## [1]  1  2  3 10 20  5
```

- you can assign names to the elements of a vector

```r
x <- c(red="Huey", blue="Dewey", green="Louie")
x
```

```
##     red    blue   green 
##  "Huey" "Dewey" "Louie"
```

- you can get and set the names of a vector using the `names()` function

```r
names(x)
```

```
## [1] "red"   "blue"  "green"
```

- all of the elements of a vector must be of the same type
- if you combine vectors of different types the elements will be converted to the closest common type
- logical values are converted to numeric values


```r
c(FALSE, 3)
```

```
## [1] 0 3
```

- numeric values are converted to strings


```r
c(pi,"abc")
```

```
## [1] "3.14159265358979" "abc"
```

- logical values are converted to strings


```r
c(FALSE, "abc")
```

```
## [1] "FALSE" "abc"
```

- the **sequence** function `seq()` creates a vector of equally spaced values


```r
seq(4, 9)
```

```
## [1] 4 5 6 7 8 9
```

- you can specify the step size


```r
seq(4, 10, 2)
```

```
## [1]  4  6  8 10
```

- you could have created the `hh` vector used in our BMI graph as follows


```r
seq(1.65, 1.90, 0.05)
```

```
## [1] 1.65 1.70 1.75 1.80 1.85 1.90
```

- when the step size is `1` you can use an abbreviation


```r
4:9
```

```
## [1] 4 5 6 7 8 9
```

- the **replicate** function `rep()` repeats values


```r
rep(1:2, c(10, 15))
```

```
##  [1] 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
```

- use the **each** named argument to repeat all values by the same amount


```r
rep(1:2, each=10)
```

```
##  [1] 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2
```

## 1.2.7 Matrices and arrays

- R supports multi-dimensional arrays of data
    - a vector is a 1-dimensional array
    - a matrix is a 2-dimensional array
- refer to <https://cran.r-project.org/doc/manuals/r-release/R-intro.pdf> for more information about arrays
- R represents arrays as vectors with a dimension attribute `dim()`
    - the shape of an array is given by a dimension vector
    - an n-dimensional array has a dimension vector of length n


```r
x <- 1:12
dim(x) <- c(3, 4)
x
```

```
##      [,1] [,2] [,3] [,4]
## [1,]    1    4    7   10
## [2,]    2    5    8   11
## [3,]    3    6    9   12
```

- by default the matrix is filled with data in column-major order
- use `matrix()` to create a matrix in one step


```r
matrix(1:12, nrow=3, byrow=T)
```

```
##      [,1] [,2] [,3] [,4]
## [1,]    1    2    3    4
## [2,]    5    6    7    8
## [3,]    9   10   11   12
```

- the rows and columns can be given names using `rownames()` and `colnames()`


```r
rownames(x) <- LETTERS[1:3]
x
```

```
##   [,1] [,2] [,3] [,4]
## A    1    4    7   10
## B    2    5    8   11
## C    3    6    9   12
```

- `LETTERS` is a character vector that contains the capital letters A-Z


```r
LETTERS
```

```
##  [1] "A" "B" "C" "D" "E" "F" "G" "H" "I" "J" "K" "L" "M" "N" "O" "P" "Q"
## [18] "R" "S" "T" "U" "V" "W" "X" "Y" "Z"
```

- `letters` contains the small letters a-z


```r
letters
```

```
##  [1] "a" "b" "c" "d" "e" "f" "g" "h" "i" "j" "k" "l" "m" "n" "o" "p" "q"
## [18] "r" "s" "t" "u" "v" "w" "x" "y" "z"
```

- `month.name` contains the month names


```r
month.name
```

```
##  [1] "January"   "February"  "March"     "April"     "May"      
##  [6] "June"      "July"      "August"    "September" "October"  
## [11] "November"  "December"
```

- `month.abb` contains the month abbreviations


```r
month.abb
```

```
##  [1] "Jan" "Feb" "Mar" "Apr" "May" "Jun" "Jul" "Aug" "Sep" "Oct" "Nov"
## [12] "Dec"
```

- transpose a matrix using `t()`


```r
t(x)
```

```
##       A  B  C
## [1,]  1  2  3
## [2,]  4  5  6
## [3,]  7  8  9
## [4,] 10 11 12
```

- vectors can be combined to form matrices
- use `cbind()` to combine vectors column-wise


```r
cbind(A=1:4, B=5:8, C=9:12)
```

```
##      A B  C
## [1,] 1 5  9
## [2,] 2 6 10
## [3,] 3 7 11
## [4,] 4 8 12
```

- use `rbind()` to combine vectors row-wise


```r
rbind(A=1:4, B=5:8, C=9:12)
```

```
##   [,1] [,2] [,3] [,4]
## A    1    2    3    4
## B    5    6    7    8
## C    9   10   11   12
```

## 1.2.8 Factors

- non-quantitative statistical data may be **categorical**
    - e.g. hair colour, political party, gender
- often categorical data is coded numerically
    - it is important to distinguish between numerically coded categorical data and quantitative data
- R let's you treat numerically coded data as categorical data using **factors**
- a factor has a set of named **levels**


```r
pain <- c(0, 3, 2, 2, 1)
fpain <- factor(pain, levels=0:3)
levels(fpain) <- c("none", "mild", "medium", "severe")
fpain
```

```
## [1] none   severe medium medium mild  
## Levels: none mild medium severe
```

- extract the numeric coding using `as.numeric()`


```r
as.numeric(fpain)
```

```
## [1] 1 4 3 3 2
```

- use `ordered()` instead of `factor()` to create an ordered factor

## 1.2.9 Lists

- a **list** is a collection of named objects
- the elements of a list may be other lists
- create a list using `list()`


```r
intake.pre <- c(5260,5470,5640,6180,6390,6515,6805,7515,7515,8230,8770)
intake.post <- c(3910,4220,3885,5160,5645,4680,5265,5975,6790,6900,7335)
mylist <- list(before=intake.pre, after=intake.post)
mylist
```

```
## $before
##  [1] 5260 5470 5640 6180 6390 6515 6805 7515 7515 8230 8770
## 
## $after
##  [1] 3910 4220 3885 5160 5645 4680 5265 5975 6790 6900 7335
```

- you can access the elements of a list using `$`


```r
mylist$before
```

```
##  [1] 5260 5470 5640 6180 6390 6515 6805 7515 7515 8230 8770
```

- many R functions return lists

## 1.2.10 Data frames

- an R **data frame** is a list of vectors and factors, all of the same length
    - these are displayed as columns
- a data frame is used to store measurements or observations on a sequence of experimental units
- data values at the same position in each vector or factor correspond to the same experimental unit
    - these are displayed as rows
    - each row has a unique name
- create a data frame from data using `data.frame()`


```r
d <- data.frame(intake.pre, intake.post)
d
```

```
##    intake.pre intake.post
## 1        5260        3910
## 2        5470        4220
## 3        5640        3885
## 4        6180        5160
## 5        6390        5645
## 6        6515        4680
## 7        6805        5265
## 8        7515        5975
## 9        7515        6790
## 10       8230        6900
## 11       8770        7335
```

- access the **components** of the data frame using `$` as for lists

```r
d$intake.pre
```

```
##  [1] 5260 5470 5640 6180 6390 6515 6805 7515 7515 8230 8770
```

## 1.2.11 Indexing

- you can select an element of a vector by **indexing** it with square brackets (`[]`)
    - indexing is also referred to as **subsetting**
- the value of the index is the position of the element in the vector, starting from `1`


```r
intake.pre[5]
```

```
## [1] 6390
```

- you can assign a new value to an element of a vector by indexing the element


```r
intake.pre[5] <- 6390
```

- you can index a vector using a vector of positions


```r
intake.pre[c(3, 5, 7)]
```

```
## [1] 5640 6390 6805
```

- you must use a vector to index a vector
    - e.g. `index.pre[3, 5, 7]` is how you index one element of a 3-dimensional array
- you can index using variables


```r
v <- c(3, 5, 7)
intake.pre[v]
```

```
## [1] 5640 6390 6805
```

- you can use the sequence notation `a:b`


```r
intake.pre[1:5]
```

```
## [1] 5260 5470 5640 6180 6390
```

- you can omit elements using negative indexes


```r
intake.pre[-c(3, 5, 7)]
```

```
## [1] 5260 5470 6180 6515 7515 7515 8230 8770
```

- you cannot mix negative and positive indexes

## 1.2.12 Conditional selection

- you can extract data from a vector using a logical expression


```r
intake.post[intake.pre > 7000]
```

```
## [1] 5975 6790 6900 7335
```

- R defines the following **comparison operators** which produce logical values

Operator | Meaning
-------- | -------------------------------
`x < y`  | x is less than y
`x > y`  | x is greater than y
`x == y` | x is equal to y
`x <= y` | x is less than or equal to y
`x >= y` | x is greater than or equal to y
`x != y` | x is not equal to y

- you can combine logical expressions using the following **logical operators**

Operator| Meaning | Detail
------- | ------- | ---------------------------------------------------------------
`x & y` | x and y | `TRUE` if both x and y are `TRUE`, otherwise `FALSE`
`x | y` | x or y  | `TRUE` if at least one of x and y are `TRUE`, otherwise `FALSE`
`!x`    | not x   | `TRUE` if x is `FALSE`, `FALSE` if x is `TRUE`


```r
intake.post[intake.pre > 7000 & intake.pre <= 8000]
```

```
## [1] 5975 6790
```

- a relational expression that describes some condition produces a logical vector
    - indexing with a logical vector selects the elements that have `TRUE` in their position


```r
intake.pre > 7000 & intake.pre <= 8000
```

```
##  [1] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE FALSE FALSE
```

- if the logical vector contains `NA` then the selected value is `NA`


```r
c(3, 5, 7)[c(TRUE, FALSE, NA)]
```

```
## [1]  3 NA
```

- comparisons with `NA` produce `NA`


```r
c(TRUE, FALSE, NA) == NA
```

```
## [1] NA NA NA
```

- to test for `NA` values use `is.na()` which produces `TRUE` for `NA` and `FALSE` otherwise


```r
is.na(c(TRUE, FALSE, NA))
```

```
## [1] FALSE FALSE  TRUE
```

## 1.2.13 Indexing of data frames


```r
d <- data.frame(intake.pre,intake.post)
head(d)
```

```
##   intake.pre intake.post
## 1       5260        3910
## 2       5470        4220
## 3       5640        3885
## 4       6180        5160
## 5       6390        5645
## 6       6515        4680
```

- you can access a data frame like a list


```r
d$intake.post
```

```
##  [1] 3910 4220 3885 5160 5645 4680 5265 5975 6790 6900 7335
```

- use can index a data frame like a matrix
    - e.g. select the data value in row 5, column 1

```r
d[5,1]
```

```
## [1] 6390
```

- you can select an entire row


```r
d[5,]
```

```
##   intake.pre intake.post
## 5       6390        5645
```

- you can select an entire column


```r
d[,2]
```

```
##  [1] 3910 4220 3885 5160 5645 4680 5265 5975 6790 6900 7335
```

- you can subset the data frame


```r
d[2]
```

```
##    intake.post
## 1         3910
## 2         4220
## 3         3885
## 4         5160
## 5         5645
## 6         4680
## 7         5265
## 8         5975
## 9         6790
## 10        6900
## 11        7335
```

- conditional selection is useful for extracting a subset of rows


```r
d[d$intake.pre > 7000,]
```

```
##    intake.pre intake.post
## 8        7515        5975
## 9        7515        6790
## 10       8230        6900
## 11       8770        7335
```

- recall that the expression produces a logical vector


```r
sel <- d$intake.pre > 7000
d[sel,]
```

```
##    intake.pre intake.post
## 8        7515        5975
## 9        7515        6790
## 10       8230        6900
## 11       8770        7335
```

- you can select the first few rows using a sequence of row numbers


```r
d[1:2,]
```

```
##   intake.pre intake.post
## 1       5260        3910
## 2       5470        4220
```

- print the first few rows using `head()`


```r
head(d)
```

```
##   intake.pre intake.post
## 1       5260        3910
## 2       5470        4220
## 3       5640        3885
## 4       6180        5160
## 5       6390        5645
## 6       6515        4680
```

- print the last few rows using `tail()`


```r
tail(d)
```

```
##    intake.pre intake.post
## 6        6515        4680
## 7        6805        5265
## 8        7515        5975
## 9        7515        6790
## 10       8230        6900
## 11       8770        7335
```

## 1.2.14 Grouped data and data frames

- the natural way to store grouped data is to use a data frame that has the measurements in a numeric column and the group in a factor column
    - e.g. consider the energy expenditure for women, grouped by stature


```r
energy
```

```
##    expend stature
## 1    9.21   obese
## 2    7.53    lean
## 3    7.48    lean
## 4    8.08    lean
## 5    8.09    lean
## 6   10.15    lean
## 7    8.40    lean
## 8   10.88    lean
## 9    6.13    lean
## 10   7.90    lean
## 11  11.51   obese
## 12  12.79   obese
## 13   7.05    lean
## 14  11.85   obese
## 15   9.97   obese
## 16   7.48    lean
## 17   8.79   obese
## 18   9.69   obese
## 19   9.68   obese
## 20   7.58    lean
## 21   9.19   obese
## 22   8.11    lean
```

- you can extract the measurements for each group


```r
exp.lean <- energy$expend[energy$stature == "lean"]
exp.lean
```

```
##  [1]  7.53  7.48  8.08  8.09 10.15  8.40 10.88  6.13  7.90  7.05  7.48
## [12]  7.58  8.11
```

```r
exp.obese <- energy$expend[energy$stature == "obese"]
exp.obese
```

```
## [1]  9.21 11.51 12.79 11.85  9.97  8.79  9.69  9.68  9.19
```

- use `split()` to split a vector into a list of vectors, one for each group


```r
l <- split(energy$expend, energy$stature)
l
```

```
## $lean
##  [1]  7.53  7.48  8.08  8.09 10.15  8.40 10.88  6.13  7.90  7.05  7.48
## [12]  7.58  8.11
## 
## $obese
## [1]  9.21 11.51 12.79 11.85  9.97  8.79  9.69  9.68  9.19
```

## 1.2.15 Implicit loops

- R has the same looping constructs found in most programming languages
- R also provides functions that perform implicit looping
- a common use case is to apply a function to each element of a set and collect the results into a list
- consider the `thuesen` data frame


```r
head(thuesen)
```

```
##   blood.glucose short.velocity
## 1          15.3           1.76
## 2          10.8           1.34
## 3           8.1           1.27
## 4          19.5           1.47
## 5           7.2           1.27
## 6           5.3           1.49
```

- `lapply()` collects the results into a list
    - e.g. compute the mean of each column of a data frame, removing `NA` values


```r
lapply(thuesen, mean, na.rm=T)
```

```
## $blood.glucose
## [1] 10.3
## 
## $short.velocity
## [1] 1.325652
```

- `sapply()` is like `lapply()` except that it simplifies the result into a vector or matrix if possible


```r
sapply(thuesen, mean, na.rm=T)
```

```
##  blood.glucose short.velocity 
##      10.300000       1.325652
```

- another common use case is to repeat a computation a number of times and collect the result into a vector
    - e.g. **simulation** using random numbers
    - this can be done using `sapply()`
    - `replicate()` is a simpler alternative
    

```r
replicate(10, mean(rexp(20)))
```

```
##  [1] 1.1323868 0.6178480 0.7700334 1.2152589 0.9759322 1.0542755 1.1673273
##  [8] 0.9944366 0.7445958 1.2206261
```

- use `apply()` to apply a function to the rows or columns of a matrix
    - or along a dimension of a multi-dimensional array
- e.g. find the minimum value in each column of a 4 x 3 matrix

```r
m <- matrix(rnorm(12), 4)
m
```

```
##            [,1]       [,2]       [,3]
## [1,] -0.2794526 -0.7633141 -0.9598333
## [2,]  1.8334284 -1.6179113 -0.4505036
## [3,]  0.4534225  0.9483115 -0.7690545
## [4,]  0.8558124 -1.6217478 -0.2912981
```

```r
apply(m, 2, min)
```

```
## [1] -0.2794526 -1.6217478 -0.9598333
```

- `tapply()` produces a table of results obtained by applying a function to groups of data values
    - the vector of data values is the first argument
    - the grouping factor, or list of grouping factors, is the second argument
    - the dimension of the table is equal to the number of grouping factors


```r
tapply(energy$expend, energy$stature, median)
```

```
##  lean obese 
##  7.90  9.69
```

## 1.2.16 Sorting

- use `sort()` to sort a vector


```r
intake$post
```

```
##  [1] 3910 4220 3885 5160 5645 4680 5265 5975 6790 6900 7335
```

```r
sort(intake$post)
```

```
##  [1] 3885 3910 4220 4680 5160 5265 5645 5975 6790 6900 7335
```

- sometimes you need to sort a collection of variables based on the order of some other variables
    - e.g. sort blood pressure by sex and age
- use `order()` to compute the positions of the variables when sorted


```r
order(intake$post)
```

```
##  [1]  3  1  2  6  4  7  5  8  9 10 11
```

- to sort the other variables, index them by the result of `order()`


```r
o <- order(intake$post)
intake$post[o]
```

```
##  [1] 3885 3910 4220 4680 5160 5265 5645 5975 6790 6900 7335
```

```r
intake$pre[o]
```

```
##  [1] 5640 5260 5470 6515 6180 6805 6390 7515 7515 8230 8770
```

- you can sort an entire data frame by reordering its rows


```r
intake.sorted <- intake[o,]
intake.sorted
```

```
##     pre post
## 3  5640 3885
## 1  5260 3910
## 2  5470 4220
## 6  6515 4680
## 4  6180 5160
## 7  6805 5265
## 5  6390 5645
## 8  7515 5975
## 9  7515 6790
## 10 8230 6900
## 11 8770 7335
```

- you can sort by multiple variables by passing them as arguments to `order()`
    - e.g. `order(sex, age)` sorts first by `sex`, then, within groups of the same sex, by `age`
    
    
## 1.3 Exercises

1.1 How would you check whether two vectors are the same if they may contain missing (NA) values? (Use of the identical function is considered cheating!)

ANSWER: Use `is.na()` to test for `NA` values. 
The vectors must have the same length.
First compare the positions of all `NA` values.
Then compare the remaining not `NA` values for equality.


```r
same <- function(x,y) {
  length(x) == length(y) &&
    all(is.na(x) == is.na(y)) &&
    all(x[!is.na(x)] == y[!is.na(y)])
}
v1 <- c(1, 2, 3)
same(v1,v1)
```

```
## [1] TRUE
```

```r
v2 <- c(1, 2, 3, 4)
v3 <- c(1, 2, 3, NA)
same(v2,v3)
```

```
## [1] FALSE
```

```r
same(v3,v3)
```

```
## [1] TRUE
```

1.2 If x is a factor with n levels and y is a length n vector, what happens if you compute y[x]?

ANSWER: The factor x behaves like a vector of numeric indices from 1 to n.


```r
x <- as.factor(c("low", "low", "medium", "high", "low"))
x
```

```
## [1] low    low    medium high   low   
## Levels: high low medium
```

```r
y <- c("red", "green", "blue")
y[x]
```

```
## [1] "green" "green" "blue"  "red"   "green"
```

1.3 Write the logical expression to use to extract girls between 7 and 14
years of age in the juul data set.

ANSWER: Age may be `NA` so test that using `is.na()` in addition to the age bounds.


```r
head(juul)
```

```
##    age menarche sex igf1 tanner testvol
## 1   NA       NA  NA   90     NA      NA
## 2   NA       NA  NA   88     NA      NA
## 3   NA       NA  NA  164     NA      NA
## 4   NA       NA  NA  166     NA      NA
## 5   NA       NA  NA  131     NA      NA
## 6 0.17       NA   1  101      1      NA
```

```r
juul.7.14 <- juul[!is.na(juul$age) & juul$age >= 7 & juul$age <= 14,]
head(juul.7.14)
```

```
##      age menarche sex igf1 tanner testvol
## 99  7.01       NA   1   NA      1       1
## 100 7.04       NA   1  149      1       1
## 101 7.07       NA   1   NA      1       1
## 102 7.07       NA   1  187      1       1
## 103 7.08       NA   1   NA      1       1
## 104 7.22       NA   1  103      1       1
```

1.4 What happens if you change the levels of a factor (with levels) and
give the same value to two or more levels?

ANSWER: R replaces the old levels with the new levels.
This effectively merges levels that are given the same name.


```r
severity <- c("low", "high", "major", "low")
fseverity <- as.factor(severity)
fseverity
```

```
## [1] low   high  major low  
## Levels: high low major
```

```r
levels(fseverity)
```

```
## [1] "high"  "low"   "major"
```

```r
levels(fseverity) <- c("high","low","high")
fseverity
```

```
## [1] low  high high low 
## Levels: high low
```

1.5 On p. 27, replicate was used to simulate the distribution of the mean of 20 random numbers from the exponential distribution by repeating the operation 10 times. How would you do the same thing with sapply?

ANSWER: 
`sapply()` takes a list as its first argument so give it a vector of length 10.
`sapply()` takes a function as its second argument so wrap `mean(rexp(20)` in a function.


```r
replicate(10,mean(rexp(20)))
```

```
##  [1] 0.6926296 0.8502073 0.7976227 1.0389594 0.9189372 0.5682124 1.3092608
##  [8] 0.9086292 0.8514561 0.8045924
```

```r
sapply(1:10, function(x) mean(rexp(20)))
```

```
##  [1] 0.8506643 1.1662770 1.0469674 0.4931616 1.2429348 1.0964285 1.3239393
##  [8] 1.1036552 1.1872367 0.5849917
```
