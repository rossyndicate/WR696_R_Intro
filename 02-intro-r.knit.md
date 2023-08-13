# Introduction to R and RStudio


## Getting to know RStudio

When you first open RStudio, it is split into 3 panels:

-   **The Console** (left), where you can directly type and run code (by hitting Enter)
-   **The Environment/History pane** (upper-right), where you can view the objects you currently have stored in your environment and a history of the code you've run
-   **The Files/Plots/Packages/Help pane** (lower-right), where you can search for files, view and save your plots, view and manage what packages are loaded in your library and session, and get R help

![Image Credit: Software Carpentry](https://swcarpentry.github.io/r-novice-gapminder/fig/01-rstudio.png){alt="Image Credit: Software Carpentry" width="100%"}

<br>

To write and save code you use **scripts**. You can open a new script with File -\> New File -\> R Script or by clicking the icon with the green plus sign in the upper left corner under 'File'. When you open a script, RStudio then opens a fourth **'Source' panel** in the upper-left to write and save your code. You can also send code from a script directly to the console to execute it by highlighting the **entire** code line/chunk (or place your cursor at the very end of the code chunk) and hit CTRL+ENTER on a PC or CMD+ENTER on a Mac.

![Image Credit: Software Carpentry](https://swcarpentry.github.io/r-novice-gapminder/fig/01-rstudio-script.png){alt="Image Credit: Software Carpentry"}

It is good practice to add comments/notes throughout your scripts to document what the code is doing. To do this start your text with a `#`. R knows to ignore everything after a `#`, so you can write whatever you want there. Note that R reads line by line, so if you want your comments to carry over multiple lines you need a `#` at every line.

## R Projects

As a first step whenever you start a new project, workflow, analysis, etc., it is good practice to set up an R project. R Projects are RStudio's way of bundling together all your files for a specific project, such as data, scripts, results, figures. Your project directory also becomes your working directory, so everything is self-contained and easily portable.

We recommend using a single R Project for this course, so lets create one now.

You can start an R project in an existing directory or in a new one. To create a project go to File -\> New Project:

![](images/project-start.png)

Let's choose 'New Directory' then 'New Project'. Now choose a directory name, this will be both the folder name and the project name, so use proper spelling conventions (no spaces!). We recommend naming it something course specific, like 'ESS-330-2023'. Choose where on your local file system you want to save this new folder/project, then click 'Create Project'.

Now you can see your RStudio session is working in the R project you just created. You can see the working directory printed at the top of your console is now the project directory, and in the 'Files' tab in RStudio you can see there is an .Rproj file with the same name as the R project, which will open up this R project in RStudio whenever you come back to it.

**Test out how this .Rproj file works**. Close out of your R session, navigate to the project folder on your computer, and double-click the .Rproj file.

::: {.alert .alert-info}
***What is a working directory?*** A working directory is the default file path to a specific file location on your computer to read files from or save files to. Since everyone's computer is unique, everyone's full file paths will be different. This is an advantage of working in R Projects, you can use *relative* file paths, since the working directory defaults to wherever the .RProj file is saved on your computer you don't need to specify the full unique path to read and write files within the project directory.
:::

## Write your first script

Let's start coding!

The first thing you do in a fresh R session and at the beginning of a workfow is set up your environment, which mostly includes installing and loading necessary libraries and reading in required data sets. Let's open a fresh R script and save it in our root (project) directory. Call this script something like 'r-intro.R'.

### Commenting code

It is best practice to add comments throughout your code noting what you are doing at each step. This is helpful for both future you (say you forgot what a chunk of code is doing after returning to it months later) and for others you may share your code with.

To comment out code you use a `#`. You can use as many `#`'s as you want, any thing you write on that line after at least one `#` will be read as a comment and R will know to ignore that and not try to execute it as code.

At the top of your script, write some details about the script like a title, your name and date.


```r
# Introduction to R and RStudio
# your name
# date
```

Now for the rest of this lesson, write all the code in this script you just created. You can execute code from a script (i.e., send it from the script to the console) in various ways (see below). Think of these scripts as your code notes, you can write and execute code, add notes throughout, and then save it and come back to it whenever you want.

### Executing code

Almost always you will start a script by installing and/or loading all the libraries/packages you need for that workflow. Add the following lines of code to your script to import our R packages you should have already installed from the [R Setup](01-R-setup.Rmd) page.


```r
#load necessary libraries
library(tidyverse)
```

```
## Warning: package 'tidyverse' was built under R version 4.2.3
```

```
## Warning: package 'ggplot2' was built under R version 4.2.3
```

```
## Warning: package 'tibble' was built under R version 4.2.3
```

```
## Warning: package 'tidyr' was built under R version 4.2.3
```

```
## Warning: package 'readr' was built under R version 4.2.3
```

```
## Warning: package 'dplyr' was built under R version 4.2.3
```

```
## Warning: package 'forcats' was built under R version 4.2.3
```

```
## Warning: package 'lubridate' was built under R version 4.2.3
```

```
## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
## ✔ dplyr     1.1.1     ✔ readr     2.1.4
## ✔ forcats   1.0.0     ✔ stringr   1.5.0
## ✔ ggplot2   3.4.1     ✔ tibble    3.2.1
## ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
## ✔ purrr     1.0.1     
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```

```r
library(palmerpenguins)
```

To execute code you can either highlight the entire line(s) of code you want to run and click the 'Run' button in the upper-right of the Source pane or use the keyboard shortcut CTRL+Enter on Windows or CMD+Enter on Macs.

You can also place your cursor at the very end of the line or chunk of code you want to run and hit CTRL+Enter or CMD+Enter.

::: {.alert .alert-info}
All functions and other code chunks must properly close all parentheses or brackets to execute. If you have an un-closed parentheses/bracket you will get stuck in a never ending loop and will keep seeing `+` printed in the console. To get out of this loop you can either close the parentheses or bracket, or hit ESC to start over. You want to make sure you see the `>` in the console and not the `+` to execute code.
:::

### Getting help with code

Take advantage of the 'Help' pane in RStudio! There you can search packages and specific functions to see all the available and required arguments, along with the default argument settings and some code examples. You can also execute a help search from the console with a `?`. For example:


```r
?mean
```

```
## starting httpd help server ... done
```

### Functions

R has many built in functions to perform various tasks. To run these functions you type the function name followed by parentheses. Within the parentheses you put in your specific arguments needed to run the function.

Practice running these various functions and see what output is printed in the console.


```r
# mathematical functions with numbers
log(10)
```

```
## [1] 2.302585
```

```r
# average a range of numbers
mean(1:5)
```

```
## [1] 3
```

```r
# nested functions for a string of numbers, using the concatenate function 'c'
mean(c(1,2,3,4,5))
```

```
## [1] 3
```

```r
# functions with characters
print("Hello World")
```

```
## [1] "Hello World"
```

```r
paste("Hello", "World", sep = "-")
```

```
## [1] "Hello-World"
```

#### Assignment operator

Notice that when you ran the following functions above, the answers were printed to the console, but were not saved anywhere (i.e., you don't see them stored as variables in your environment). To save the output of some operation to your environment you use the assignment operator `<-`. For example, run the following line of code:


```r
x <- log(10)
```

And now you see the output, '2.3025...' saved as a variable named 'x'. You can now use this value in other functions


```r
x + 5
```

```
## [1] 7.302585
```

#### Base R vs. The Tidyverse

You may hear the terms 'Base R' and 'Tidyverse' a lot throughout this course. Base R includes functions that are installed with the R software and do not require the installation of additional packages to use them. The Tidyverse is a collection of R packages designed for data manipulation, exploration, and visualization that you are likely to use in every day data analysis, and all use the same design philosophy, grammar, and data structures. When you install the Tidyverse, it installs all of these packages, and you can then load all of them in your R session with `library(tidyverse)`. Base R and Tidyverse have many similar functions, but many prefer the style, efficiency and functionality of the Tidyverse packages, and we will mostly be sticking to Tidyverse functions for this course.

### Data Types

For this intro lesson, we are going to use the Palmer Penguins data set (which is loaded with the `palmerpenguins` package you installed during setup). This data was collected and made available by [Dr. Kristen Gorman](https://www.uaf.edu/cfos/people/faculty/detail/kristen-gorman.php) and the [Palmer Station, Antarctica LTER](https://pallter.marine.rutgers.edu/), a member of the [Long Term Ecological Research Network](https://lternet.edu/).

Load the `penguins` data set.


```r
data("penguins")
```

You now see it in the Environment pane. Print it to the console to see a snapshot of the data:


```r
penguins
```

```
## # A tibble: 344 × 8
##    species island    bill_length_mm bill_depth_mm flipper_…¹ body_…² sex    year
##    <fct>   <fct>              <dbl>         <dbl>      <int>   <int> <fct> <int>
##  1 Adelie  Torgersen           39.1          18.7        181    3750 male   2007
##  2 Adelie  Torgersen           39.5          17.4        186    3800 fema…  2007
##  3 Adelie  Torgersen           40.3          18          195    3250 fema…  2007
##  4 Adelie  Torgersen           NA            NA           NA      NA <NA>   2007
##  5 Adelie  Torgersen           36.7          19.3        193    3450 fema…  2007
##  6 Adelie  Torgersen           39.3          20.6        190    3650 male   2007
##  7 Adelie  Torgersen           38.9          17.8        181    3625 fema…  2007
##  8 Adelie  Torgersen           39.2          19.6        195    4675 male   2007
##  9 Adelie  Torgersen           34.1          18.1        193    3475 <NA>   2007
## 10 Adelie  Torgersen           42            20.2        190    4250 <NA>   2007
## # … with 334 more rows, and abbreviated variable names ¹​flipper_length_mm,
## #   ²​body_mass_g
```

This data is structured is a data frame, probably the most common data type and one you are most familiar with. These are like the spreadsheets you worked with in the first lesson, tabular data organized by rows and columns. However we see at the top this is called a `tibble` which is just a fancy kind of data frame specific to the `tidyvese`.

At the top we can see the data type of each column. There are five main data types:

-   **character**: `"a"`, `"swc"`

-   **numeric**: `2`, `15.5`

-   **integer**: `2L` (the `L` tells R to store this as an integer, otherwise integers can also be numeric data types)

-   **logical**: `TRUE`, `FALSE`

-   **complex**: `1+4i` (complex numbers with real and imaginary parts)

Data types are combined to form data structures. R's basic data structures include

-   atomic vector

-   list

-   matrix

-   data frame

-   factors

You can see the data type or structure of an object using the `class()` function, and get more specific details using the `str()` function. (Note that 'tbl' stands for tibble).


```r
class(penguins)
```

```
## [1] "tbl_df"     "tbl"        "data.frame"
```

```r
str(penguins)
```

```
## tibble [344 × 8] (S3: tbl_df/tbl/data.frame)
##  $ species          : Factor w/ 3 levels "Adelie","Chinstrap",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ island           : Factor w/ 3 levels "Biscoe","Dream",..: 3 3 3 3 3 3 3 3 3 3 ...
##  $ bill_length_mm   : num [1:344] 39.1 39.5 40.3 NA 36.7 39.3 38.9 39.2 34.1 42 ...
##  $ bill_depth_mm    : num [1:344] 18.7 17.4 18 NA 19.3 20.6 17.8 19.6 18.1 20.2 ...
##  $ flipper_length_mm: int [1:344] 181 186 195 NA 193 190 181 195 193 190 ...
##  $ body_mass_g      : int [1:344] 3750 3800 3250 NA 3450 3650 3625 4675 3475 4250 ...
##  $ sex              : Factor w/ 2 levels "female","male": 2 1 1 NA 1 2 1 2 NA NA ...
##  $ year             : int [1:344] 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 ...
```


```r
class(penguins$species)
```

```
## [1] "factor"
```

```r
str(penguins$species)
```

```
##  Factor w/ 3 levels "Adelie","Chinstrap",..: 1 1 1 1 1 1 1 1 1 1 ...
```

When we pull one column from a data frame, like we just did above with the `$` operator, that returns a vector. Vectors are 1-dimensional, and must contain data of a single data type (i.e., you cannot have a vector of both numbers and characters).

If you want a 1-dimensional object that holds mixed data types and structures, that would be a list. You can put together pretty much anything in a list.


```r
myList <- list("apple", 1993, FALSE, penguins)
str(myList)
```

```
## List of 4
##  $ : chr "apple"
##  $ : num 1993
##  $ : logi FALSE
##  $ : tibble [344 × 8] (S3: tbl_df/tbl/data.frame)
##   ..$ species          : Factor w/ 3 levels "Adelie","Chinstrap",..: 1 1 1 1 1 1 1 1 1 1 ...
##   ..$ island           : Factor w/ 3 levels "Biscoe","Dream",..: 3 3 3 3 3 3 3 3 3 3 ...
##   ..$ bill_length_mm   : num [1:344] 39.1 39.5 40.3 NA 36.7 39.3 38.9 39.2 34.1 42 ...
##   ..$ bill_depth_mm    : num [1:344] 18.7 17.4 18 NA 19.3 20.6 17.8 19.6 18.1 20.2 ...
##   ..$ flipper_length_mm: int [1:344] 181 186 195 NA 193 190 181 195 193 190 ...
##   ..$ body_mass_g      : int [1:344] 3750 3800 3250 NA 3450 3650 3625 4675 3475 4250 ...
##   ..$ sex              : Factor w/ 2 levels "female","male": 2 1 1 NA 1 2 1 2 NA NA ...
##   ..$ year             : int [1:344] 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 ...
```

You can even nest lists within lists


```r
list(myList, list("more stuff here", list("and more")))
```

```
## [[1]]
## [[1]][[1]]
## [1] "apple"
## 
## [[1]][[2]]
## [1] 1993
## 
## [[1]][[3]]
## [1] FALSE
## 
## [[1]][[4]]
## # A tibble: 344 × 8
##    species island    bill_length_mm bill_depth_mm flipper_…¹ body_…² sex    year
##    <fct>   <fct>              <dbl>         <dbl>      <int>   <int> <fct> <int>
##  1 Adelie  Torgersen           39.1          18.7        181    3750 male   2007
##  2 Adelie  Torgersen           39.5          17.4        186    3800 fema…  2007
##  3 Adelie  Torgersen           40.3          18          195    3250 fema…  2007
##  4 Adelie  Torgersen           NA            NA           NA      NA <NA>   2007
##  5 Adelie  Torgersen           36.7          19.3        193    3450 fema…  2007
##  6 Adelie  Torgersen           39.3          20.6        190    3650 male   2007
##  7 Adelie  Torgersen           38.9          17.8        181    3625 fema…  2007
##  8 Adelie  Torgersen           39.2          19.6        195    4675 male   2007
##  9 Adelie  Torgersen           34.1          18.1        193    3475 <NA>   2007
## 10 Adelie  Torgersen           42            20.2        190    4250 <NA>   2007
## # … with 334 more rows, and abbreviated variable names ¹​flipper_length_mm,
## #   ²​body_mass_g
## 
## 
## [[2]]
## [[2]][[1]]
## [1] "more stuff here"
## 
## [[2]][[2]]
## [[2]][[2]][[1]]
## [1] "and more"
```

You can use the `names()` function to retrieve or assign names to list and vector elements


```r
names(myList) <- c("fruit", "year", "logic", "data")
names(myList)
```

```
## [1] "fruit" "year"  "logic" "data"
```

### Indexing

Indexing is an extremely important aspect to data exploration and manipulation. In fact you already started indexing when we looked at the data type of individual columns with `penguins$species`. How you index is dependent on the data structure.

Index lists:


```r
# for lists we use double brackes [[]]
myList[[1]]
```

```
## [1] "apple"
```

```r
myList[["data"]]
```

```
## # A tibble: 344 × 8
##    species island    bill_length_mm bill_depth_mm flipper_…¹ body_…² sex    year
##    <fct>   <fct>              <dbl>         <dbl>      <int>   <int> <fct> <int>
##  1 Adelie  Torgersen           39.1          18.7        181    3750 male   2007
##  2 Adelie  Torgersen           39.5          17.4        186    3800 fema…  2007
##  3 Adelie  Torgersen           40.3          18          195    3250 fema…  2007
##  4 Adelie  Torgersen           NA            NA           NA      NA <NA>   2007
##  5 Adelie  Torgersen           36.7          19.3        193    3450 fema…  2007
##  6 Adelie  Torgersen           39.3          20.6        190    3650 male   2007
##  7 Adelie  Torgersen           38.9          17.8        181    3625 fema…  2007
##  8 Adelie  Torgersen           39.2          19.6        195    4675 male   2007
##  9 Adelie  Torgersen           34.1          18.1        193    3475 <NA>   2007
## 10 Adelie  Torgersen           42            20.2        190    4250 <NA>   2007
## # … with 334 more rows, and abbreviated variable names ¹​flipper_length_mm,
## #   ²​body_mass_g
```

Index vectors:


```r
# for vectors we use single brackets []
myVector <- c("apple", "banana", "pear")
myVector[2]
```

```
## [1] "banana"
```

Index data frames:


```r
# dataframe[row(s), columns()]
penguins[1:5, 2]
```

```
## # A tibble: 5 × 1
##   island   
##   <fct>    
## 1 Torgersen
## 2 Torgersen
## 3 Torgersen
## 4 Torgersen
## 5 Torgersen
```

```r
penguins[1:5, "island"]
```

```
## # A tibble: 5 × 1
##   island   
##   <fct>    
## 1 Torgersen
## 2 Torgersen
## 3 Torgersen
## 4 Torgersen
## 5 Torgersen
```

```r
penguins[1, 1:5]
```

```
## # A tibble: 1 × 5
##   species island    bill_length_mm bill_depth_mm flipper_length_mm
##   <fct>   <fct>              <dbl>         <dbl>             <int>
## 1 Adelie  Torgersen           39.1          18.7               181
```

```r
penguins[1:5, c("species","sex")]
```

```
## # A tibble: 5 × 2
##   species sex   
##   <fct>   <fct> 
## 1 Adelie  male  
## 2 Adelie  female
## 3 Adelie  female
## 4 Adelie  <NA>  
## 5 Adelie  female
```

```r
penguins[penguins$sex=='female',]
```

```
## # A tibble: 176 × 8
##    species island    bill_length_mm bill_depth_mm flipper_…¹ body_…² sex    year
##    <fct>   <fct>              <dbl>         <dbl>      <int>   <int> <fct> <int>
##  1 Adelie  Torgersen           39.5          17.4        186    3800 fema…  2007
##  2 Adelie  Torgersen           40.3          18          195    3250 fema…  2007
##  3 <NA>    <NA>                NA            NA           NA      NA <NA>     NA
##  4 Adelie  Torgersen           36.7          19.3        193    3450 fema…  2007
##  5 Adelie  Torgersen           38.9          17.8        181    3625 fema…  2007
##  6 <NA>    <NA>                NA            NA           NA      NA <NA>     NA
##  7 <NA>    <NA>                NA            NA           NA      NA <NA>     NA
##  8 <NA>    <NA>                NA            NA           NA      NA <NA>     NA
##  9 <NA>    <NA>                NA            NA           NA      NA <NA>     NA
## 10 Adelie  Torgersen           41.1          17.6        182    3200 fema…  2007
## # … with 166 more rows, and abbreviated variable names ¹​flipper_length_mm,
## #   ²​body_mass_g
```

```r
# $ for a single column
penguins$species
```

```
##   [1] Adelie    Adelie    Adelie    Adelie    Adelie    Adelie    Adelie   
##   [8] Adelie    Adelie    Adelie    Adelie    Adelie    Adelie    Adelie   
##  [15] Adelie    Adelie    Adelie    Adelie    Adelie    Adelie    Adelie   
##  [22] Adelie    Adelie    Adelie    Adelie    Adelie    Adelie    Adelie   
##  [29] Adelie    Adelie    Adelie    Adelie    Adelie    Adelie    Adelie   
##  [36] Adelie    Adelie    Adelie    Adelie    Adelie    Adelie    Adelie   
##  [43] Adelie    Adelie    Adelie    Adelie    Adelie    Adelie    Adelie   
##  [50] Adelie    Adelie    Adelie    Adelie    Adelie    Adelie    Adelie   
##  [57] Adelie    Adelie    Adelie    Adelie    Adelie    Adelie    Adelie   
##  [64] Adelie    Adelie    Adelie    Adelie    Adelie    Adelie    Adelie   
##  [71] Adelie    Adelie    Adelie    Adelie    Adelie    Adelie    Adelie   
##  [78] Adelie    Adelie    Adelie    Adelie    Adelie    Adelie    Adelie   
##  [85] Adelie    Adelie    Adelie    Adelie    Adelie    Adelie    Adelie   
##  [92] Adelie    Adelie    Adelie    Adelie    Adelie    Adelie    Adelie   
##  [99] Adelie    Adelie    Adelie    Adelie    Adelie    Adelie    Adelie   
## [106] Adelie    Adelie    Adelie    Adelie    Adelie    Adelie    Adelie   
## [113] Adelie    Adelie    Adelie    Adelie    Adelie    Adelie    Adelie   
## [120] Adelie    Adelie    Adelie    Adelie    Adelie    Adelie    Adelie   
## [127] Adelie    Adelie    Adelie    Adelie    Adelie    Adelie    Adelie   
## [134] Adelie    Adelie    Adelie    Adelie    Adelie    Adelie    Adelie   
## [141] Adelie    Adelie    Adelie    Adelie    Adelie    Adelie    Adelie   
## [148] Adelie    Adelie    Adelie    Adelie    Adelie    Gentoo    Gentoo   
## [155] Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo   
## [162] Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo   
## [169] Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo   
## [176] Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo   
## [183] Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo   
## [190] Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo   
## [197] Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo   
## [204] Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo   
## [211] Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo   
## [218] Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo   
## [225] Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo   
## [232] Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo   
## [239] Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo   
## [246] Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo   
## [253] Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo   
## [260] Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo   
## [267] Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo    Gentoo   
## [274] Gentoo    Gentoo    Gentoo    Chinstrap Chinstrap Chinstrap Chinstrap
## [281] Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap
## [288] Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap
## [295] Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap
## [302] Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap
## [309] Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap
## [316] Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap
## [323] Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap
## [330] Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap
## [337] Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap Chinstrap
## [344] Chinstrap
## Levels: Adelie Chinstrap Gentoo
```

### Read and Write Data

We used an R data package today to read in our data frame, but that probably isn't how you will normally read in your data. There are many ways to read and write data in R. To read in .csv files, you can use `read_csv()` which is included in the Tidyverse with the `readr` package, and to save csv files use `write_csv()`. The `readxl` package is great for reading in excel files, however it is not included in the Tidyverse and will need to be loaded separately.

Find the .csv you created at the end of last week's lesson. Created a folder in your project directory called 'data/' and copy the .csv file there. You will store various data sets in this 'data/' folder throughout the course.

Say your .csv is called 'survey_data_clean.csv'. This is how you would read it in to R, giving it the object name 'survey_data'









