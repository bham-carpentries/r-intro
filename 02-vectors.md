---
title: Vectors
teaching: 15
exercises: 10
source: Rmd
---

::::::::::::::::::::::::::::::::::::::: objectives

- Understand vectorized operations in R.
- Obtain basic vector summaries
- Extract elements from a vector: by index, by name, using comparison operations
- Skip and remove elements from a vector

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- What is a vector in R?
- How can I operate on vectors?
- How can I get information about vectors?
- How can I select data from a vector?

::::::::::::::::::::::::::::::::::::::::::::::::::



## Vectors in R

A vector allows us to work with several values at once. Technically, a 
vector is 1 dimensional array of values of the same data type. For example, 
a number sequence:


``` r
1:5
```

``` output
[1] 1 2 3 4 5
```

We can assign a vector to a variable:


``` r
x <- 5:10
```

We can also create vectors "by hand" using the `c()` function; this tersely named function is used to _combine_ values into a vector; these values can, themselves, be vectors:


``` r
c(2, 4, -1)
```

``` output
[1]  2  4 -1
```

``` r
c(x, 2, 2, 3)
```

``` output
[1]  5  6  7  8  9 10  2  2  3
```

Vectors aren't limited to storing numbers:


``` r
c("a", "b", "c", "def")
```

``` output
[1] "a"   "b"   "c"   "def"
```

The elements of vectors can also have names, they can be given by prepending 
them to the values, separated by an equals sign:


``` r
prices <- c(coffee = 3.50, tea = 2.50, cake = 4.00)
```

## Vectorization

R is *vectorized*, meaning that we can apply functions to all the elements of a vector, 
for example mathematical operators:


``` r
(1:5) * 2
```

``` output
[1]  2  4  6  8 10
```

``` r
2^(1:5)
```

``` output
[1]  2  4  8 16 32
```

or comparison operators


``` r
y <- 10:12
y == 11
```

``` output
[1] FALSE  TRUE FALSE
```

## Special values

There are three special values that can be included in a vector:

* `NA` represents a "not available", or "missing" value. 
* `NaN` represents something that is "Not a Number" or "undefined", e.g. `1/0`.
* `Inf` represents an infinite value (`-Inf` represents negative infinity).

### Handling special values

If we perform computations which include NA, the result is usually NA:


``` r
x + NA
```

``` output
[1] NA NA NA NA NA NA
```

This raises an interesting point; how do we test if vector values are missing? This doesn’t work:


``` r
y <- c(2, 4, NA)
y == NA
```

``` output
[1] NA NA NA
```

There are a number of special functions you can use to handle special values:

 * `is.na` will return all positions in a vector containing `NA`.
 * `is.nan`, and `is.infinite` will do the same for `NaN` and `Inf`.
 * `is.finite` will return all positions in a vector
   that do not contain `NA`, `NaN` or `Inf`.
 * `na.omit` will filter out all missing values from a vector

## Built-in constants

R comes with a few built-in constants, which a vectors containing useful values:

``` r
LETTERS
letters
month.abb
month.name
```

We will use some of these in the examples that follow.

## Basic vector summaries

There are some basic functions to help us get information about vectors


``` r
length(letters)
```

``` output
[1] 26
```

``` r
head(letters, n = 2)
```

``` output
[1] "a" "b"
```

``` r
tail(letters, n = 4)
```

``` output
[1] "w" "x" "y" "z"
```


## Subsetting vectors

Having defined a vector, it's often useful to _extract_ parts of a vector.   We do this with the
`[]` operator.  Using the built in `month.name` vector:


``` r
month.name[2]
```

``` output
[1] "February"
```

``` r
month.name[2:4]
```

``` output
[1] "February" "March"    "April"   
```

Let's unpick the second example; `2:4` generates the sequence 2,3,4.   This gets passed to the 
extract operator `[]`.   We can also generate this sequence using the `c()` function:


``` r
month.name[c(2,3,4)]
```

``` output
[1] "February" "March"    "April"   
```

:::::::::::::: callout
## Vector numbering in R starts at 1

In many programming languages (C and python, for example), the first
element of a vector has an index of 0. In R, the first element is 1.
::::::::::::::

Values are returned in the order that we specify the indices.  We can extract the same element more 
than once:


``` r
month.name[4:2]
```

``` output
[1] "April"    "March"    "February"
```

``` r
month.name[c(1,1,2,3,4)]
```

``` output
[1] "January"  "January"  "February" "March"    "April"   
```

If we try and extract an element that doesn't exist in the vector, the missing values are `NA`:


``` r
month.name[10:13]
```

``` output
[1] "October"  "November" "December" NA        
```

### Skipping and removing elements

If we use a negative number as the index of a vector, R will return
every element *except* for the one specified:


``` r
month.name[-2]
```

``` output
 [1] "January"   "March"     "April"     "May"       "June"      "July"     
 [7] "August"    "September" "October"   "November"  "December" 
```

We can skip multiple elements:


``` r
month.name[c(-1, -5)]  # or month.name[-c(1,5)]
```

``` output
 [1] "February"  "March"     "April"     "June"      "July"      "August"   
 [7] "September" "October"   "November"  "December" 
```

:::::::::::::::::::: callout
## Tip: Order of operations

A common error occurs when trying to skip
slices of a vector. Most people first try to negate a
sequence like so:


``` r
month.name[-1:3]
```

This gives a somewhat cryptic error:


``` error
Error in `month.name[-1:3]`:
! only 0's may be mixed with negative subscripts
```

But remember the order of operations. `:` is really a function, so
what happens is it takes its first argument as -1, and second as 3,
so generates the sequence of numbers: `-1, 0, 1, 2, 3`.

The correct solution is to wrap that function call in brackets, so
that the `-` operator is applied to the sequence:


``` r
-(1:3)
```

``` output
[1] -1 -2 -3
```

``` r
month.name[-(1:3)]
```

``` output
[1] "April"     "May"       "June"      "July"      "August"    "September"
[7] "October"   "November"  "December" 
```
::::::::::::::::::::

### Subsetting with names

We can also access elements by their name:


``` r
prices["cake"]
```

``` output
cake 
   4 
```

``` r
prices[c("coffee", "tea")]
```

``` output
coffee    tea 
   3.5    2.5 
```

### Subsetting with logical vectors 

As well as providing a list of indices we want to keep (or delete, if we prefix them with `-`), we 
can pass a _logical vector_ to R indicating the indices we wish to select:


``` r
fourmonths <- month.name[1:4]
fourmonths
```

``` output
[1] "January"  "February" "March"    "April"   
```

``` r
fourmonths[c(TRUE, FALSE, TRUE, TRUE)]
```

``` output
[1] "January" "March"   "April"  
```

What happens if we supply a logical vector that is shorter than the vector we're extracting the elements from?


``` r
fourmonths[c(TRUE,FALSE)]
```

``` output
[1] "January" "March"  
```

This illustrates the idea of _vector recycling_; the `[]` extract operator "recycles" the subsetting vector:


``` r
fourmonths[c(TRUE,FALSE,TRUE,FALSE)]
```

``` output
[1] "January" "March"  
```

This can be useful, but can easily catch you out.

The idea of selecting elements of a vector using a logical subsetting vector may seem a bit esoteric, and a lot more
typing than just selecting the elements you want by index.  It becomes really useful when we write code to generate
the logical vector:


``` r
my_vector <- c(0.01, 0.69, 0.51, 0.39)
my_vector > 0.5
```

``` output
[1] FALSE  TRUE  TRUE FALSE
```

``` r
my_vector[my_vector > 0.5]
```

``` output
[1] 0.69 0.51
```

:::::::::::: callout
## Tip: Combining logical conditions

There are many situations in which you will wish to combine multiple logical
criteria. For example, we might want to find all the elements that are 
between two values. Several operations for combining logical vectors exist in R:

+ `&`, the "logical AND" operator: returns `TRUE` if both the left and right
  are `TRUE`.
+ `|`, the "logical OR" operator: returns `TRUE`, if either the left or right
  (or both) are `TRUE`.

The recycling rule applies with both of these, so `TRUE & c(TRUE, FALSE, TRUE)`
will compare the first `TRUE` on the left of the `&` sign with each of the
three conditions on the right.

You may sometimes see `&&` and `||` instead of `&` and `|`. These operators
do not use the recycling rule: they only look at the first element of each
vector and ignore the remaining elements. The longer operators are mainly used
in programming, rather than data analysis.

+ `!`, the "logical NOT" operator: converts `TRUE` to `FALSE` and `FALSE` to
  `TRUE`. It can negate a single logical condition (e.g. `!TRUE` becomes
  `FALSE`), or a whole vector of conditions(e.g. `!c(TRUE, FALSE)` becomes
  `c(FALSE, TRUE)`).

Additionally, you can compare the elements within a single vector using the
`all` function (which returns `TRUE` if every element of the vector is `TRUE`)
and the `any` function (which returns `TRUE` if one or more elements of the
vector are `TRUE`).
::::::::::::

:::::::::::: challenge
## Challenge 1

Return a vector containing the letters of the alphabet in reverse order

:::::::::::::::  solution
## Solution to challenge 1
We can extract the elements in reverse order by generating the sequence
26, 25, ... 1 using the `:` operator:


``` r
letters[26:1]
```

``` output
 [1] "z" "y" "x" "w" "v" "u" "t" "s" "r" "q" "p" "o" "n" "m" "l" "k" "j" "i" "h"
[20] "g" "f" "e" "d" "c" "b" "a"
```

Although this works, it makes the assumption that `letters` will always be length 26.
Although this is probably a safe assumption in English, other
languages may have more (or fewer) letters in their alphabet.   It is good
practice to avoid assuming _anything_ about your data.

We can avoid assuming `letters` is length 26, by using the `length()` function:


``` r
letters[length(letters):1]
```

``` output
 [1] "z" "y" "x" "w" "v" "u" "t" "s" "r" "q" "p" "o" "n" "m" "l" "k" "j" "i" "h"
[20] "g" "f" "e" "d" "c" "b" "a"
```
:::::::::::::::
:::::::::::::::::::::::::::::


:::::::::::::::::::::::::::::::::::::::  challenge

## Challenge 2

Given the following code:


``` r
x <- c(5.4, 6.2, 7.1, 7.5, 4.8)
x
```

``` output
[1] 5.4 6.2 7.1 7.5 4.8
```

Come up with at least 3 different commands that will produce the following output:


``` output
[1] 6.2 7.1 7.5
```

After you find 3 different commands, compare notes with your neighbour. Did you have different strategies?

:::::::::::: solution
## Solution to challenge 2


``` r
x[2:4]
```

``` output
[1] 6.2 7.1 7.5
```

``` r
x[-c(1,5)]
```

``` output
[1] 6.2 7.1 7.5
```

``` r
x[c(2,3,4)]
```

``` output
[1] 6.2 7.1 7.5
```



``` r
x[c(FALSE, TRUE, TRUE, TRUE, FALSE)]
```

``` output
[1] 6.2 7.1 7.5
```

We can construct a logical test to generate the logical vector:

``` r
x[x > 6]
```

``` output
[1] 6.2 7.1 7.5
```
Unpicking this example, `x > 6` generates the logical vector:


``` output
[1] FALSE  TRUE  TRUE  TRUE FALSE
```

Which is passed to the `[ ]` subsetting operator.
:::::::::::::::::::
:::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Indexing in R starts at 1, not 0.
- Access individual values by location using `[]`.
- Access slices of data using `[low:high]`.
- Access arbitrary sets of data using `[c(...)]`.
- Use logical vectors to access subsets of data meeting certain criteria.

::::::::::::::::::::::::::::::::::::::::::::::::::
