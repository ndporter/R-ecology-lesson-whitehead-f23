---
title: Introduction to R
author: Data Carpentry contributors & Nathaniel Porter
teaching: 15
Exercises: 15
---



------------------------------------------------------------------------

::: objectives
### Learning Objectives

-   Define the following terms as they relate to R: object, assign, call, function, arguments, options.
-   Create objects and assign values to them in R.
-   Learn how to *name* objects.
-   Save a script file for later use.
-   Use comments to inform script.
-   Solve simple arithmetic operations in R.
-   Call functions and use arguments to change their default options.
-   Inspect the content of vectors and manipulate their content.
-   Subset and extract values from vectors.
-   Analyze vectors with missing data.
:::

------------------------------------------------------------------------

*Note: This lesson is a shortened version of the [Data Carpentry Ecology R Lesson](https://datacarpentry.org/R-ecology-lesson). Please refer to the original for additional functions and examples, as well as regular updates.*

## Creating objects in R



You can get output from R simply by typing math in the console:


```r
3 + 5
12 / 7
```

However, to do useful and interesting things, we need to assign *values* to *objects*. To create an object, we need to give it a name followed by the assignment operator `<-`, and the value we want to give it:


```r
weight_kg <- 55
```

`<-` is the assignment operator. It assigns values on the right to objects on the left. So, after executing `x <- 3`, the value of `x` is `3`. For historical reasons, you can also use `=` for assignments, but not in every context. Because of the [slight](https://blog.revolutionanalytics.com/2008/12/use-equals-or-arrow-for-assignment.html) [differences](https://renkun.me/2014/01/28/difference-between-assignment-operators-in-r/) in syntax, it is good practice to always use `<-` for assignments.

Objects can be given almost any name such as `x`, `current_temperature`, or `subject_id`. Here are some further guidelines on naming objects:

-   You want your object names to be explicit and not too long.
-   They cannot start with a number (`2x` is not valid, but `x2` is).
-   R is case sensitive, so for example, `weight_kg` is different from `Weight_kg`.
-   Don't use function names of fundamental functions in R (e.g., `if`, `else`, `for`, `c`, `T`, `mean`, `data`, `df`, `weights`, etc.). If in doubt, check the help to see if the name is already in use.
-   Avoid dots (`.`) within names.
-   Be consistent in the styling of your code, such as where you put spaces, how you name objects, etc. Styles can include "lower_snake", "UPPER_SNAKE", "lowerCamelCase", "UpperCamelCase", etc.

::: callout
### Objects vs. variables

What are known as `objects` in `R` are known as `variables` in many other programming languages. Depending on the context, `object` and `variable` can have drastically different meanings. However, in this lesson, the two words are used synonymously. For more information see: <https://cran.r-project.org/doc/manuals/r-release/R-lang.html#Objects>
:::

When assigning a value to an object, R does not print anything. You can force R to print the value by typing the object name:


```r
weight_kg <- 55    # doesn't print anything
weight_kg          # but typing the name of the object does (once it's created)
```

Now that R has `weight_kg` in memory, we can do arithmetic with it. For instance, we may want to convert this weight into pounds (weight in pounds is 2.2 times the weight in kg):


```r
2.2 * weight_kg
```

We can also change an object's value by assigning it a new one:


```r
weight_kg <- 57.5
2.2 * weight_kg
```

Assigning a value to one object does not change the values of other objects. For example, let's store the animal's weight in pounds in a new object, `weight_lb`:


```r
weight_lb <- 2.2 * weight_kg
```

and then change `weight_kg` to 100.


```r
weight_kg <- 100
```

What do you think is the current content of the object `weight_lb`? 126.5 or 220?

### Saving your code

Up to now, your code has been in the console. This is useful for quick queries but not so helpful if you want to revisit your work for any reason.

The easiest way to ensure your R code (scripts) works seamlessly with data and other files is to create a project with `File - New Project`. Choose `New Directory` and `New Project` then choose a location for the folder and create the project.

Create a script in your new project by pressing <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>N</kbd>. It is wise to save your script file immediately. To do this press <kbd>Ctrl</kbd> + <kbd>S</kbd>. This will open a dialogue box where you can decide where to save your script file, and what to name it. The `.R` file extension is added automatically and ensures your file will open with RStudio.

Don't forget to save your work periodically by pressing <kbd>Ctrl</kbd> + <kbd>S</kbd>.

### Comments

The comment character in R is `#`. Anything to the right of a `#` in a script will be ignored by R. It is useful to leave notes and explanations in your scripts. For convenience, RStudio provides a keyboard shortcut to comment or uncomment a paragraph: after selecting the lines you want to comment, press at the same time on your keyboard <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>C</kbd>. If you only want to comment out one line, you can put the cursor at any location of that line (i.e. no need to select the whole line), then press <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>C</kbd>.



```r
# This line is a comment and doesn't cause a problem
2 * 3 #this comment doesn't either
But this line will produce an error
```

```{.error}
#> Error: <text>:3:5: unexpected symbol
#> 2: 2 * 3 #this comment doesn't either
#> 3: But this
#>        ^
```

### Functions and their arguments

Functions are "canned scripts" that automate more complicated sets of commands including operations assignments, etc. Many functions are predefined, or can be made available by importing R *packages* (more on that later). A function usually takes one or more inputs called *arguments*. Functions often (but not always) return a *value*. A typical example would be the function `round()`. The input (the argument) must be a number, and the return value (in fact, the output) is the input rounded to the nearest whole number. Executing a function ('running it') is called *calling* the function. An example of a function call is:


```r
round(3.14159)
```

```{.output}
#> [1] 3
```

Here, we've called `round()` with just one argument, `3.14159`, and it has returned the value `3`. That's because the default is to round to the nearest whole number.

The return 'value' of a function need not be numerical, and it also does not need to be a single item: it can be a set of things, or even a dataset. We'll see that when we read data files into R.

Arguments can be anything, not only numbers or filenames, but also other objects. Exactly what each argument means differs per function, and must be looked up in the documentation (see below). Some functions take arguments which may either be specified by the user, or, if left out, take on a *default* value: these are called *options*. Options are typically used to alter the way the function operates, such as whether it ignores 'bad values', or what symbol to use in a plot. However, if you want something specific, you can specify a value of your choice which will be used instead of the default.

If we want more digits we can see how to do that by getting information about the `round` function. We can use `args(round)` to find what arguments it takes, or look at the help for this function using `?round`.


```r
args(round)
```

```{.output}
#> function (x, digits = 0) 
#> NULL
```


```r
?round
```

We see that if we want a different number of digits, we can type `digits = 2` or however many we want.


```r
round(3.14159, digits = 2)
```

```{.output}
#> [1] 3.14
```

If you provide the arguments in the exact same order as they are defined you don't have to name them:


```r
round(3.14159, 2)
```

```{.output}
#> [1] 3.14
```

And if you do name the arguments, you can switch their order:


```r
round(digits = 2, x = 3.14159)
```

```{.output}
#> [1] 3.14
```

It's good practice to put the non-optional arguments (like the number you're rounding) first in your function call, and to then specify the names of all optional arguments. If you don't, someone reading your code might have to look up the definition of a function with unfamiliar arguments to understand what you're doing.

## Vectors and data types

A vector is the most common and basic data type in R, and is pretty much the workhorse of R. A vector is composed by a series of values, which can be either numbers or characters. We can assign a series of values to a vector using the `c()` function. For example we can create a vector of animal weights and assign it to a new object `weight_g`:


```r
weight_g <- c(50, 60, 65, 82)
weight_g
```

A vector can also contain characters:


```r
animals <- c("mouse", "rat", "dog")
animals
```

The quotes around "mouse", "rat", etc. are essential here. Without the quotes R will assume objects have been created called `mouse`, `rat` and `dog`. As these objects don't exist in R's memory, there will be an error message.

There are many functions that allow you to inspect the content of a vector. `length()` tells you how many elements are in a particular vector:


```r
length(weight_g)
length(animals) #notice this doesn't return the number of characters
```

An important feature of a vector, is that all of the elements are the same type of data. The function `class()` indicates what kind of object you are working with:


```r
class(weight_g)
class(animals)
```

The function `str()` provides an overview of the structure of an object and its elements. It is a useful function when working with large and complex objects:


```r
str(weight_g)
str(animals)
```

You can use the `c()` function to add other elements to your vector:


```r
weight_g <- c(weight_g, 90) # add to the end of the vector
weight_g <- c(30, weight_g) # add to the beginning of the vector
weight_g
```

In the first line, we take the original vector `weight_g`, add the value `90` to the end of it, and save the result back into `weight_g`. Then we add the value `30` to the beginning, again saving the result back into `weight_g`.

We can do this over and over again to grow a vector, or assemble a dataset. As we program, this may be useful to add results that we are collecting or calculating.

An **atomic vector** is the simplest R **data type** and is a linear vector of a single type. Above, we saw 2 of the 6 main **atomic vector** types that R uses: `"character"` and `"numeric"` (or `"double"`). These are the basic building blocks that all R objects are built from. The other 4 **atomic vector** types are:

-   `"logical"` for `TRUE` and `FALSE` (the boolean data type)
-   `"integer"` for integer numbers (e.g., `2L`, the `L` indicates to R that it's an integer)
-   `"complex"` to represent complex numbers with real and imaginary parts (e.g., `1 + 4i`) and that's all we're going to say about them
-   `"raw"` for bitstreams that we won't discuss further

You can check the type of your vector using the `typeof()` function and inputting your vector as the argument.

Vectors are one of the many **data structures** that R uses. Other important types you may encounter are lists (`list`), matrices (`matrix`), data frames (`data.frame`), factors (`factor`) and arrays (`array`).

::: challenge
### Challenge

-   We've seen that atomic vectors can be of type character, numeric (or double), integer, and logical. But what happens if we try to mix these types in a single vector?

::: solution
R implicitly converts them to all be the same type
:::

-   What will happen in each of these examples? (hint: use `class()` to check the data type of your objects):

    ``` r
    num_char <- c(1, 2, 3, "a")
    num_logical <- c(1, 2, 3, TRUE)
    char_logical <- c("a", "b", "c", TRUE)
    tricky <- c(1, 2, 3, "4")
    ```

-   Why do you think it happens?

::: solution
Vectors can be of only one data type. R tries to convert (coerce) the content of this vector to find a "common denominator" that doesn't lose any information.
:::

-   How many values in `combined_logical` are `"TRUE"` (as a character) in the following example (reusing the 2 `..._logical`s from above):

    ``` r
    combined_logical <- c(num_logical, char_logical)
    ```

::: solution
Only one. There is no memory of past data types, and the coercion happens the first time the vector is evaluated. Therefore, the `TRUE` in `num_logical` gets converted into a `1` before it gets converted into `"1"` in `combined_logical`.
:::

-   You've probably noticed that objects of different types get converted into a single, shared type within a vector. In R, we call converting objects from one class into another class *coercion*. These conversions happen according to a hierarchy, whereby some types get preferentially coerced into other types. Can you draw a diagram that represents the hierarchy of how these data types are coerced?

::: solution
logical → numeric → character ← logical
:::
:::



## Subsetting vectors

If we want to extract one or several values from a vector, we must provide one or several indices in square brackets. For instance:


```r
animals <- c("mouse", "rat", "dog", "cat")
animals[2]
```

```{.output}
#> [1] "rat"
```

```r
animals[c(3, 2)]
```

```{.output}
#> [1] "dog" "rat"
```

::: callout

### Program in other languages?

R indices start at 1. Some other languages (like C++, Java, Perl, and Python) count from 0 because that's simpler for computers to do.
:::

### Conditional subsetting

Another common way of subsetting is by selecting only values where a condition is `TRUE`. To do so, we use the `[]` notation with a logical test:


```r
## we can use this to select only the values above 50
weight_g[weight_g > 50]
```

```{.output}
#> [1] 60 65 82 90
```

You can combine multiple tests using `&` (both conditions are true, AND) or `|` (at least one of the conditions is true, OR):


```r
weight_g[weight_g > 30 & weight_g < 50]
```

```{.output}
#> numeric(0)
```

```r
weight_g[weight_g <= 30 | weight_g == 55]
```

```{.output}
#> [1] 30
```

```r
weight_g[weight_g >= 30 & weight_g == 21]
```

```{.output}
#> numeric(0)
```

Here, `>` for "greater than", `<` stands for "less than", `<=` for "less than or equal to", and `==` for "equal to". The double equal sign `==` is a test for numerical equality between the left and right hand sides, and should not be confused with the single `=` sign, which performs variable assignment (similar to `<-`).

A common task is to search for certain strings in a vector. One could use the "or" operator `|` to test for equality to multiple values, but this can quickly become tedious. The function `%in%` allows you to test if any of the elements of a search vector are found:


```r
animals <- c("mouse", "rat", "dog", "cat", "cat")

# use the logical vector created by %in% to return elements from animals
# that are found in the character vector
animals[animals %in% c("rat", "cat", "dog")]
```

```{.output}
#> [1] "rat" "dog" "cat" "cat"
```

## Missing data

As R was designed to analyze datasets, it includes the concept of missing data (which is uncommon in other programming languages). Missing data are represented in vectors as `NA`.

When doing operations on numbers, most functions will return `NA` if the data you are working with include missing values. This feature makes it harder to overlook the cases where you are dealing with missing data. You can add the argument `na.rm = TRUE` to calculate the result as if the missing values were removed (`rm` stands for ReMoved) first.


```r
heights <- c(2, 4, 4, NA, 6)
mean(heights)
max(heights)
mean(heights, na.rm = TRUE)
max(heights, na.rm = TRUE)
```

If your data include missing values, you may want to become familiar with the functions `is.na()`, `na.omit()`, and `complete.cases()`. See below for examples.


```r
## Extract those elements which are not missing values.
heights[!is.na(heights)]

## Returns the object with incomplete cases removed.
#The returned object is an atomic vector of type `"numeric"` (or #`"double"`).
na.omit(heights)

## Extract those elements which are complete cases.
#The returned object is an atomic vector of type `"numeric"` (or #`"double"`).
heights[complete.cases(heights)]
```

Recall that you can use the `typeof()` function to find the type of your atomic vector.

::: challenge
### Challenge

1.  Using this vector of heights in inches, create a new vector, `heights_no_na`, with the NAs removed.

``` r
heights <- c(63, 69, 60, 65, NA, 68, 61, 70, 61, 59, 64, 69, 63, 63, NA, 72, 65, 64, 70, 63, 65)
```

2.  Use the function `median()` to calculate the median of the `heights` vector.

3.  Use R to figure out how many people in the set are taller than 67 inches.

::: solution

```r
heights <- c(63, 69, 60, 65, NA, 68, 61, 70, 61, 59, 64, 69, 63, 63, NA, 72, 65, 64, 70, 63, 65)

# 1.
heights_no_na <- heights[!is.na(heights)]
# or
heights_no_na <- na.omit(heights)
# or
heights_no_na <- heights[complete.cases(heights)]

# 2.
median(heights, na.rm = TRUE)

# 3.
heights_above_67 <- heights_no_na[heights_no_na > 67]
length(heights_above_67)
```
:::
:::



Now that we have learned how to write scripts, and the basics of R's data structures, we are ready to start working with a real dataset and learn about data frames.
