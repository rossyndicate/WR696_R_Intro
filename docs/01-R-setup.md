# Setup Instructions

This tutorial walks you through all the **required** setup steps for using R and RStudio in this course. Please use our class's Teams Channel to post any questions/problems that you encounter.


## Install R and RStudio

**R** is an open source language and software environment for statistical analysis and graphics (plus so much more!). You must **first download the R software (for free) here: <https://www.r-project.org/>.**

-   Click the download link based on your operating system (OS). Then, for Mac users, install the latest release based on your macOS. For Windows users, click the 'install R for the first time' link.

*Note: If you already have R installed, you **must have at least version 4.0.0. or greater**, but it is best to have the most recent version installed (4.3.1)*

**RStudio** is a (also free) R Integrated Development Environment (IDE) that provides a built-in editor and other advantages such as version control and project management. **Once you have the R software installed on your computer, you can install RStudio Desktop here: <https://posit.co/download/rstudio-desktop/>.**

-   Under **Step 2** click the download RStudio Desktop button.

## Package Installation

While the R software comes with many pre-loaded functions (referred to as 'base R' functions) to perform various operations in R, there are thousands of R packages that provide additional reusable R functions. In order to use these functions you need to first install the package to your local machine using the `install.packages()` function. Once a package is installed on your computer you don't need to install it again (but you may have to update it). Anytime you want to use the package in a new R session you can load it with the `library()` function.

We will be working in RStudio for this entire course, so after you have installed both R and RStudio, **open a new session of RStudio.**

You will learn more about the ins and outs of RStudio in class, but for set up purposes you will just be running code in the Console. Normally you want to save the code you write, but since package installation is only needed once (unless you are working on a new machine or need to update any packages) you can execute this directly in the console.

Run the following three lines of code (one at a time) in the console. *You can click the copy button in the upper right corner when you hover over the code chunk, then paste that after the `>` in the Console. Spelling and capitalization is important!*

**Install the {tidyverse} package.** The Tidyverse is actually a collection of multiple R packages designed for data manipulation, exploration, and visualization that you are likely to use in every day data analysis. When you install the Tidyverse, it installs all of these packages, and you can later load all of them in your R session with `library(tidyverse).` Since you are installing multiple packages here this may take a little while.


```r
install.packages("tidyverse")
```

**Install the {palmerpenguins} package.** This is a data package that installs a couple of spreadsheets you can load and work with in R.


```r
install.packages("palmerpenguins")
```

**Install the {rmarkdown} package**. Later on in the course you will be working in and rendering R Markdown files and reports. R Markdown is a notebook style interface integrating text and code, allowing you to create fully reproducible documents and render them to various elegantly formatted static or dynamic outputs.

You can learn more about R Markdown at their website, which has really informative lessons on their [Getting Started](https://rmarkdown.rstudio.com/lesson-1.html) page, and see the range of outputs you can create at their [Gallery](https://rmarkdown.rstudio.com/gallery.html) page.


```r
install.packages("rmarkdown")
```

To see if you successfully installed all three packages, use the `library()` function to load the packages into your session. You should either see nothing printed to the console after running `library()`, or in the case of the `tidyverse` you may see some messages printed. As long as there are no `error` messages, you should be all set! Please use our class's Teams Channel for assistance if you get any error messages.


```r
library(tidyverse)
library(palmerpenguins)
library(rmarkdown)
```
