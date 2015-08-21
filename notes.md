What do data scientists do?
1. Define the question
2. Define the ideal data set
3. Determine what data you can access
4. Obtain the data
5. Clean the data
6. Exploratory data analysis (e.g., find patterns)
7. Statistical prediction/modeling
8. Interpret results
9. Challenge results
10. Synthesize/write up results
11. Create reproducible code
12. Distribute results to other people

Help

- Access help file
    - ?rnorm
- Search help files
    - help.search("rnorm")
- Get arguments
    - args("rnorm")
- See code
    - rnorm
- R reference card
    - http://cran.r-project.org/doc/contrib/Short-refcard.pdf


##Analytics
- Descriptive: understanding what is happening/happened
- Diagnostic: understanding why things happen
- Predictive: understanding what will happen
- Prescriptive: understanding what we could do to make something happen (e.g., recommendations)

Types of questions in approximate order of difficulty
- descriptive: describe a set of data | commonly applied to census data
- exploratory: find relationships you didn't know about
               * correlation does not imply causation *
- inferential: use a relatively small sample of data to say something about a bigger population
- predictive:  to use the data on some objects to predict values for another object
               * if X predicts Y it does not mean that X causes Y
- causal:      to find what happens to one variable when you make another variable change
- mechanistic: understand the exact changes in variables that lead to changes in other
               variables for individual objects


Summary
- Good experiments
  - Have replication
  - Measure variability (high/low variability and distance between tests)
  - Generalize to the problem you care about
  - Are transparent
- Prediction is not inference
  - Both can be important
- Beware of DATA DREDGING



How to ask an R question
- What steps will reproduce the problem?
- What is the expected output?
- What do you see instead?
- Version of R
- Version of OS

Building Data Products COntent
- R packages
  - devtools
  - roxygen
  - testthat
- rCharts
- Slidify
- Shiny

Obtaining R Packages
a <- available.packages() # lots off
head(rownames(a), 3) # show the first 3

For biological applications, many packages are available from Bioconductor Project

find.packages("slidify")
install.packages("slidify")
install.packages(c("slidify","ggplot2","devtools"))
library(slidify) # load it
searchy() # show functions
find_rtools() # devtools 

... from bioconductor
source("http://bioconductor.org/biocLite.R")
biocLite()
biocLite(c("GenomicFeatures", "AnnotationDbi"))
http://www.bioconductor.org/install

Books:
- Springer
- http://www.r-project.org/doc/bib/R-books.html

Variables:
x <- 1:20 # vector
x <- 1L # integer
x <- 1 # numeric
inf = infinite

Attributes:
- name, dimnames,
- dimensions (e.g., matrices, arrays)
- class
- length
- other (custom)

# Vectors
c() can be used to create vectors of objects
x <- c(0.5, 0.6)
x <- c(TRUE, FALSE) # logical
x <- c(T, F) #logical
x <- 9:29 # integer
x <- c(1+0i, 2+4i) # complex

Mixing Objects
y <- c(1.7, "a")

# coercion occurs so that every element in the vector is of the same class, e.g., 
c(1.7, "a") == c("a", "1.7")

> x <- 0:6
> class(x)
[1] "integer"
> as.numeric(x)
[1] 0 1 2 3 4 5 6
> as.logical(x)
[1] FALSE TRUE TRUE TRUE TRUE TRUE TRUE
> as.character(x)
[1] "0" "1" "2" "3" "4" "5" "6"


# List
x <- list(1, "a", TRUE, 1 + 4i)

# Matrices
```R
> m <- matrix(nrow=2, ncol=3)
> dim(m)
[1] 2 3
> attributes(m)
$dim
[1] 2 3

> m <- matrix(1:6, nrow=2, ncol=3)

> m <- 1:10
> dim(m) <- c(2,5)

cbind && rbind
column and row, respectively
> x <- 1:3
> y <- 10:12
> cbind(x,y)
     x  y
[1,] 1  10
[2,] 2  11
[3,] 3  12

> rbind(x,y)
    [,1] [,2] [,3]
X    1    2   3
y    10   11  12
```

# Factors
Used to represent categorial data. Can be unordered or ordered. One can think of a factor as an integer vector where each integer has a label.
- Factors are treated specially by modelling functions like lm() and glm()
- Using factors with labels is better than using integers because factors are self-describing; having a variable that as values "Male" and "Female" is better than a variable that as values 1 and 2

> x <- factor(c("yes", "yes","no","yes","no"))
> x
[1] yes yes no yes no
Levels: no eyes
> table(x)
x
no  yes
2   3
> unclass(x)
[1] 2 2 1 2 1
attr(, "levels)
[1] "no"  "yes"

# Explicitly telling levels to R
# This can be important in linear modelling because the first level is used as the baseline level
> x <-factor(c("yes", "yes", "no", "yes", "no"), levels = c("yes","no"))

# Missing Values
- is.na() is used to test objects if they are NA
- is.nan() is used to test for NAN
- NA values have also a class also, so there are integers NA, characeter NA, etc.
- NaN value is also NA but the converse is not true

x <- c(1, 2, NA, 4, NA, 5)
bad <- is.na(x)
x[!bad]
[1] 1 2 4 5

x <- c(1,2,NA,4,NA,5)
y <- c("a","b"),NA,"d",NA,"f")
good <- complete.cases(x, y)
x[good]
y[good]

airquality[1:6, ] #csv file
good <- complete.cases(airquality)
airquality[good, ][1:6, ]

Subsetting
x <- c ("a", "b", "c", "c", "d", "a")
x[1]
[1] "a"

x[2]
[1] "b"

x[x > "a"]
[1] x "b" "c" "c" "d"

x[1:4]
[1] "a" "b" "c "c"

u <- x > "a"
u
[1] FALSE TRUE TRUE TRUE TRUE FALSE

x[u]
[1] "b" "c" "c" "d"


subset(x[good, ], Temp==5 & Xamps>1)



## Back to R

### Data Frames
- read.table() or read.csv() to create
- have a special attribute "row.names"
- can be converted to a matrix by calling data.matrix
> x <- data.frame(foo=1:4, bar=c(T,T,F,F))
> x
  foo bar
1   1 TRUE
2   2 TRUE
3   3 FALSE
3   3 FALSE
> nrow(x)
[1] 4
> ncol(x)
[1] 2

### Names
All R Objects can also have names

> x <- 1:3
> names(x)
NULL
> names(x) <- c("foo", "bar", "norf")
> x
foo bar norf
  1   2    3
> names(x)
[1] "foo" "bar" "norf"

And matrices:
> m <- matrix(1:4, nrow=2, ncol=2)
> dimnames(m) <- list(c("a","b"), c("c","d"))
> m
  c  d
a 1  3
b 2  4

### Reading tabular data
- read.table and read.csv (most common | difference is the separator)
  - table = " " (space)
  - csv   = "," (comma)
- readLines (to load every shit of text file)
[Analogous]
- write.table
- writeLines

### Textual dump formats
- dputing / dgeting
- dumping / sourcing

> y <- data.frame(a=1, b="a")
> y
  a b
1 1 a
> dput(y)
structure(list(a = 1, b = structure(1L, .Label = "a", class = "factor")), .Names = c("a", 
"b"), row.names = c(NA, -1L), class = "data.frame")
> dput(y, file="y.R")
> new.y <- dget("y.R")
> new.y
  a b
1 1 a
> y
  a b
1 1 a

-- dputing == 1 object
-- dumping == multiple objects

> x <- "foo"
> y <- data.frame(a=1, b="a")
> dump(c("x","y"), file="dump.R")
> rm(x,y)
> source("dump.R")
> x
[1] "foo"
> y
  a b
1 1 a

### Connections: interfaces to the outside world
- file
- gzfile
- bz2file
- url

### Indexes
x <- c("a", "b")
- Numerical
> x[0]
"a"

- Logical
> x[x > "a"]
"b"

### Subsetting
- []
- [[]]
- $name

### Subsetting Matrices
> x <- matrix(1:6,2,3)
> x
     [,1] [,2] [,3]
[1,]    1    3    5
[2,]    2    4    6
> x[1,2]
[1] 3
> x[1,]
[1] 1 3 5
> x[,2]
[1] 3 4
> x[,2, drop=FALSE]
     [,1]
[1,]    3
[2,]    4
> x[,2, drop=F]
     [,1]
[1,]    3
[2,]    4

### Subsetting Partial Matching
> x <- list(aardvark = 1:5)
> x$a
[1] 1 2 3 4 5
> x[["a"]]
NULL
> x[["a", exact = FALSE]]
[1] 1 2 3 4 5
> 

### Removing NA values
> airquality[1:6, ]
> good <- complete.cases(airquality)
> airquality[good, ][1:6, ]

### Vectorized Operations
> x <- 1:4;
> y <- 6:9;
> x + y
[1]  7  9 11 13
> x > 2
[1] FALSE FALSE  TRUE  TRUE
> x >= 2
[1] FALSE  TRUE  TRUE  TRUE
> y == 8
[1] FALSE FALSE  TRUE FALSE
> x * y
[1]  6 14 24 36
> x / y
[1] 0.1666667 0.2857143 0.3750000 0.4444444

### Vectorized Matrix Operations

> x <- matrix(1:4, 2, 2)
> x
     [,1] [,2]
[1,]    1    3
[2,]    2    4
> y <- matrix(rep(10,4), 2, 2)
> y
     [,1] [,2]
[1,]   10   10
[2,]   10   10
> x * y  # element-wise multiplication
     [,1] [,2]
[1,]   10   30
[2,]   20   40
> x / y
     [,1] [,2]
[1,]  0.1  0.3
[2,]  0.2  0.4
> x %*% y # true matrix multiplication
     [,1] [,2]
[1,]   40   40
[2,]   60   60
> 

## Loops

> for(i in 1:10){}
> for(i in 1:10){ print (i) }
[1] 1
[1] 2
[1] 3
[1] 4
[1] 5
[1] 6
[1] 7
[1] 8
[1] 9
[1] 10
> x <- c("a", "b", "c")
> seq_along(x)
[1] 1 2 3
> for(i in seq_along(x)){ print(x[i]) }
[1] "a"
[1] "b"
[1] "c"
> 
>
> for(letter in x){ print(letter) }
[1] "a"
[1] "b"
[1] "c"
>
>
> for(i in 1:4) print(x[i])
[1] "a"
[1] "b"
[1] "c"
[1] NA


- for
- while
- repeat
- next
- break
- return

## Functions

above <- function(x, n=10){
  use <- x > n
  return x[use]
}

- args()    receives a function
            outputs its argumentos
- formals() receives a function
            outputs its names

### Argument Matching
1) Check for exact match for a named argument
2) Check for a partial match
3) Check for a positional match

### The "..." argument
myplot <- function(x, y, type="1", ...){
  plot(x, y, type, ...)
}

>> "..." is often used to extend functions
  because you don't want to copy the entire
  argument list of the original function
>> "..." could be used for 'generic functions'
   that 'dispatch' methods passing everything they
   received
>> "..." good when the number of arguments are
   unknown such as cat() or paste()

One catch with "..." is that any arguments that appear
after "..." must be named explicitly and cannot be
partially matched, e.g.,

> args(paste)
function(..., sep=" ", collapse=NULL)

## Scoping
- Lexical Scoping: the values of free variables are searched for in the environment in which the function was defined
   function + environment = function closure

make.power <- function(n){
  pow <- function(x){
     x ^ n
  }
  pow
}

> cube <- make.power(3)
> cube(3)
[1] 27
> cube(2)
[1] 8
> square <- make.power(2)
> square(2)
[1] 4
> square(3)
[1] 9

ls(environment(function)) -- ex: cube

Consequences of Lexical Scoping
- in R, all objects must be stored in memory
- all functions must carry a pointer to their respective defining environments, which could be anywhere
- in S-PLUS, free variables are always looked up in the global workspace, so everything can be stored on the disk because the 'defining environment' of all functions is the same.

[[ Scoping Rules -- Optimization ]]

### Date and Time
- Dates are stored in the Date class
- Time can be stored as
    - POSIXct (integer) or
    - POSIXlt (list containing day, week, hour, etc)

  x <- as.Date("1970-01-01")
  x
  unclass(x)
- There are a number of generic functions that work on dates and times
    - weekdays: give the day of the week
    - months: give the month name
    - quarters: give the quarter number ("Q1", "Q2", "Q3", "Q4")

as.POSIXct or as.POSIXlt
x <- strptime(c("January 10, 2012 10:40"), "%B %d %Y, %H:%M")
Check ?strptime for details

# Week 3

lapply = normal map() function -- (<list>, <function>, <extra args for function>)
        returns a list
sapply = similar to lapply, but TRIES to simply the result. When not possible returns a list.
apply = (matrix, DIMENSION, function)
    shortcuts
      - rowSums = apply(x, 1, sum)
      - rowMeans = apply(x, 1, mean)
      - colSums = apply(x, 2, sum)
      - colMeans = apply(x, 2, mean)
mapply = apply to N lists in parallel
        mapply(FUN, ..., MoreArgs=NULL, SIMPLIFY=TRUE, USE.NAMES=TRUE)

tapply
 > str(tapply)
 > function(X, INDEX, FUN=NULL, ..., simplify=TRUE)

    x = vector
    index = factor or a list of factors (or else they are coerced to factors)
    FUN is a function to be applied
    ... contains others arguments to be passed to FUN
    simplify, should we simplify the result?


## Debugging
 invisible(x)

 Tools
 - traceback   => stack trace
 - debug       => flags a function for 'debug' mode
 - browser     => suspends the execution of a function and put it in debug mode
 - trace       => insert debugging code into a function specific place
 - recover     => modify the error behavior so that you can browse the call stack

