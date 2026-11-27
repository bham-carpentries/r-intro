---
title: R Packages and Seeking Help
teaching: 10
exercises: 5
source: Rmd
---

::::::::::::::::::::::::::::::::::::::: objectives

- To be able to install packages, and load them into your R session
- To be able to use CRAN task views to identify packages to solve a problem
- To be able to read R help files for functions and special operators
- To be able to seek help from your peers
- To be able to manage a workspace in an interactive R session

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions
- How do I use packages in R?
- How can I get help in R?
- How can I manage my environment?
::::::::::::::::::::::::::::::::::::::::::::::::::



## R packages

R packages extend the functionality of R.  There are thousands of packages written
by others. It's also possible to write your own packages; this can be a great way of disseminating your research and making it useful to others.  A number of useful packages are installed by default with R (are part of the R core distribution). The teaching machines at the University have a number of additional packages installed by default.

We can see the packages installed on an R installation via the "packages" tab in RStudio, or by typing `installed.packages()` at the prompt, or by selecting the "Packages" tab in RStudio.

In this course we will be using packages in the  [tidyverse](https://www.tidyverse.org) to perform the bulk of our plotting and data analysis.   Although we could do most of the tasks without using extra packages, the tidyverse makes it quicker and easier to perform common data analysis tasks.  The tidyverse packages are already installed on the university teaching machines.

## Finding and installing new packages

There are several sources of packages in R; the ones you are most likely to encounter are:

### CRAN

[CRAN](https://cran.r-project.org) is the main repository of packages for R.  All the packages have undergone basic quality assurance when they were submitted.  There are over 20,000 packages in the archive; there is a lot of overlap between some packages.  Working out _what_ the most appropriate package to use isn't always straightforward.

### Bioconductor

[Bioconductor](https://www.bioconductor.org/) is a more specialised repository, which contains packages for bioinformatics.  Common workflows are provided, and the packages are more thoroughly quality assured.   Because of its more specialised nature we don't focus on Bioconductor in this course.

### GitHub / personal websites

Some authors distribute packages via [GitHub](https://www.github.com) or their own personal web-pages.  These packages may not have undergone any form of quality assurance.   Note that many packages have their own website, but the package itself is distributed via CRAN.

### Finding packages to help with your research

There are various ways of finding packages that might be useful in your research:

* The [CRAN task view](https://cran.r-project.org/web/views/) provides an overview of the packages available for various research fields and methodologies.

* [rOpenSci](https://ropensci.org/) provides packages for performing open and reproducible science.  Most of these are available from CRAN or Bioconductor.

* Journal articles should cite the R packages they used in their analysis.

* [The Journal of Statistical Software](https://www.jstatsoft.org/index) contains peer-reviewed articles for R packages (and other statistical software).

* [The R Journal](https://journal.r-project.org/) contains articles about new packages in R.

### Installing packages

If a package is available on [CRAN](https://cran.r-project.org), you can install it by typing:


``` r
install.packages("packagename")
```

This will automatically install any packages that the package you are installing depends on.

Installing a package doesn't make the functions included in it available to you; to do this you must use the `library()` function.  As we will be using the tidyverse later in the course, let's load that now:


``` r
library("tidyverse")
```

``` output
── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
✔ dplyr     1.2.1     ✔ readr     2.2.0
✔ forcats   1.0.1     ✔ stringr   1.6.0
✔ ggplot2   4.0.4     ✔ tibble    3.3.1
✔ lubridate 1.9.5     ✔ tidyr     1.3.2
✔ purrr     1.2.2     
── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
✖ dplyr::filter() masks stats::filter()
✖ dplyr::lag()    masks stats::lag()
ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```

The tidyverse is a collection of other packages that work well together.  The `tidyverse` package's main function is to load some of these other packages.   We will be using some of these later in the course.

::: callout
## Conflicting names

You may get a warning message when loading a package that a function is "masked". This happens when a function name has already been "claimed" by a package that's already loaded.  The most recently loaded function wins.

If you want to use the function from the other package, use `packagename::function()`.
:::


## Reading Help files

R, and every package, provide help files for functions. The general syntax to search for help on any
function, say `function_name`:


``` r
?function_name
# OR
help(function_name)
```

This will load up a help page in RStudio (or by launching a web browser, or  as plain text if you are using R without RStudio).

Each help page is broken down into sections:

 - Description: An extended description of what the function does.
 - Usage: The arguments of the function and their default values.
 - Arguments: An explanation of the data each argument is expecting.
 - Details: Any important details to be aware of.
 - Value: The data the function returns.
 - See Also: Any related functions you might find useful.
 - Examples: Some examples for how to use the function.

Different functions might have different sections, but these are the main ones you should be aware of.

::: callout
## Tip: Reading help files

One of the most daunting aspects of R is the large number of functions
available. It would be prohibitive, if not impossible to remember the
correct usage for every function you use. Luckily, the help files
mean you don't have to!
:::

## Special Operators

To seek help on special operators, use quotes:


``` r
?"<-"
```

## Getting help on packages

Many packages come with "vignettes": tutorials and extended example documentation.
Without any arguments, `browseVignettes()` will open a page in your web browser with an index of all vignettes for all installed packages - this takes a few seconds to load!

To browse vignettes for a single package, use `browseVignettes(package = "package-name")`. Click on the "HTML" hyperlink next to a vignette title to open the vignette in HTML format.

If a package doesn't have any vignettes, you can usually find help by typing
`help("package-name")`, or `package?package-name`.

Posit (the company that develop RStudio) and other members of the R community 
have also provided 
[cheatsheets](https://opensource.posit.co/resources/cheatsheets/?by=&languages=R) 
for many R packages and data science tasks.

## When you kind of remember the function

If you're not sure what package a function is in, or how it's specifically spelled you can do a fuzzy search:


``` r
??function_name
```

# Other ways to get help

There are several other ways that people often get help when they are stuck with their R code.

* Search the internet: paste the last line of your error message or “R” and a short description of what you want to do into your favorite search engine and you will usually find several examples where other people have encountered the same problem and came looking for help.
* Ask somebody “in the real world”. If you have a colleague or friend with more expertise in R than you have, show them the problem you are having and ask them for help.
* Sometimes, the act of articulating your question can help you to identify what is going wrong. This is known as “rubber duck debugging” among programmers.

::: callout

Tip: Generative AI

While responses from generative AI tools can often be helpful, they are not always reliable. 
It is essential to verify the accuracy of information found this way, which requires being able to understand code as you read it and being able to fix any errors that occur when you try running code provided by genAI tools.
We recommend avoiding using genAI tools as an R beginner:

* For most beginner issues, reliable help and answers can be found through an internet search
* Trying to solve issues yourself - with the help of teaching materials and the R help files - will help you build the foundational knowledge to judge genAI responses

:::

## When your code doesn't work

Try to create a **minimal reproducible example**. Start a fresh R session and 
in a new R script, try to reproduce the problem you are facing with minimal code

* Avoid loading packages that must be installed from CRAN or elsewhere. 
    * If the issue is with a function from an add-on package, try to only load that package.
* Avoid sharing data
    * Use an in-built data set like `mtcars`
    * Create a toy data frame or other small objects (vectors, lists)

## Package versions

Many of the packages in R are frequently updated.  This does mean that code written for one version of a package may not work with another version of the package (or, potentially even worse, run but give a _different_ result).  The `sessionInfo()` command prints information about the system, and the names and versions of packages that have been loaded.  You should include the output of `sessionInfo()` somewhere in your research.




``` r
sessionInfo()
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Challenge 1

Use help to find a function (and its associated parameters) that you could
use to load data from a tabular file in which columns are delimited with "\\t"
(tab) and the decimal point is a "." (period). This check for decimal
separator is important, especially if you are working with international
colleagues, because different countries have different conventions for the
decimal point (i.e. comma vs period).
Hint: use `??"read table"` to look up functions related to reading in tabular data.

:::::::::::::::  solution

## Solution to Challenge 1

The standard R function for reading tab-delimited files with a period
decimal separator is `read.delim()`. You can also do this with
`read.table(file, sep="\t")` (the period is the *default* decimal
separator for `read.table()`). With either function, you may have to change
the `comment.char` argument if your data file contains
hash (#) characters.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Challenge 2

Vignettes are often useful tutorials.   We will be using the `dplyr` package
to manipulate tables of data.   List the vignettes available
in the package.   You might want to take a look at these now, or later when
we cover `dplyr`.

:::::::::::::::  solution

## Solution to Challenge 2



``` r
browseVignettes(package="dplyr")
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::: callout

## Citing R and R packages

If you use R in your work you should cite it, and the packages you use. The
`citation()` command will return the appropriate citation for R itself.  
`citation(packagename)` will provide the citation for `packagename`. 
In both cases, the default citation includes the version number you are currently using.

:::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Use `install.packages()` to install packages from CRAN
- Use `?` to get help on functions in R
- Use `browseVignettes()` to browse long-form package documentation 

::::::::::::::::::::::::::::::::::::::::::::::::::




