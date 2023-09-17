---
title: "Introduction to Data Analysis in R"
author: "Caitlin C. Mothes, PhD and Katie Willi"
date: "2023-09-17"
site: bookdown::bookdown_site
documentclass: book
bibliography: [book.bib, packages.bib]
url: https://ccmothes.github.io/quantitative-reasoning-course/
# cover-image: path to the social sharing image like images/cover.jpg
description: |
  This site hosts the course content for WR 696 at Colorado State University.
link-citations: yes
github-repo: rossyndicate/WR696_R_Intro
---



# Welcome!

This site hosts the course curriculum for Colorado State University's **WR 696** course: *Introduction to Data Analysis in R*

## Set up Instructions {.unnumbered}

As your first step, please follow the instructions on the [R Setup][Setup Instructions] page to make sure you have all the necessary software installed on your computer before the class starts.

## Navigating this site {.unnumbered}

The table of contents on the left allows you to navigate to the lesson for each week of the course. Each lesson will walk you through the topic(s), analysis, etc. for that week. There are exercises at the end of the lesson that will be that week's homework assignment.

Homework will be submitted through Canvas and exercise questions (including any code, figures, etc.) must be submitted as a rendered R Markdown document in Word or HTML format. The Intro to R and R Markdown lesson will walk through how to create these R Markdown documents; you will use these R Markdowns as the basis for writing your code/answers to the exercises and then render them to either a Word or HTML report which is what you will submit through Canvas.

## Goals {.unnumbered}

The broad goal of this course is to introduce you to the skills necessary for a career that involves data science - namely manipulating data sets and performing statistical tests in R. The more specific goals of this course are to teach students to:

1.  Navigate the RStudio interface and create R Markdown documents for reproducible reporting;
2.  Utilize R packages and functions to manipulate and analyze data effectively and apply data wrangling techniques using the {tidyverse} framework;
3.  Differentiate between various data types and structures within R; and
4.  Explore comparative analyses, linear regression, and trend analysis techniques to reveal patterns in data.

## Approach and Expectations {.unnumbered}

This class is [flipped](https://ieeexplore.ieee.org/document/7344151), meaning all materials for the week ahead must be reviewed before class. To encourage this we will have weekly quizzes on pre-class content each Monday before we dive into the assignment.

So without lectures in class what do we do together? We code! This class has almost four hours of contact time per week, and we design lessons so that you should be able to finish your assignments in class. The flipped class allows for deeper discussion about the common pitfalls of coding and allows for collaborative work time with your fellow classmates.

Generally we will do a quick live-code review of concepts from the assignment and the pre-class materials, but more than 1.5 hours per day will be dedicated to you coding and working on the assignment in class.

As such, coming to class is a vital part of how you can be successful and we fully expect you to be there every day.

We also will actively encourage a collaborative coding environment where students help each other and discuss the best approach to solving various coding problems. We also hope that outside of class, you will use our Teams channel to discuss code issues!

We will always send announcements with assignments, web links, and other updates through Canvas. The course syllabus will also be posted on Canvas.

## Class Schedule {.unnumbered}

+------+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Week | Data (Monday) | Content                                                                                                                                                                                                                                                              |
+------+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 1    | 8/22          | Before class: [Primers Basics](https://posit.cloud/learn/primers/1) and [R Markdown](https://rmarkdown.rstudio.com/lesson-1.html?_gl=1*10u3rje*_ga*NzUxNjg2ODAzLjE2OTE1MTIzMzk.*_ga_2C0WZ1JHG0*MTY5MTUxNjA2OC4yLjEuMTY5MTUxNjU2Ni4wLjAuMA..); download R and RStudio |
|      |               |                                                                                                                                                                                                                                                                      |
|      |               | Introduction to R, RStudio, RMarkdown                                                                                                                                                                                                                                |
+------+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 2    | 8/28          | Before class: [Work with Data](https://posit.cloud/learn/primers/2)                                                                                                                                                                                                  |
|      |               |                                                                                                                                                                                                                                                                      |
|      |               | Exploratory data analysis                                                                                                                                                                                                                                            |
+------+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 3    | 9/4           | **No Class Monday 9/4!** Before class Wednesday: [Visualize Data](https://posit.cloud/learn/primers/3)                                                                                                                                                               |
|      |               |                                                                                                                                                                                                                                                                      |
|      |               | Data visualization                                                                                                                                                                                                                                                   |
+------+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 4    | 9/11          | Before class: [Tidy Your Data](https://posit.cloud/learn/primers/4)                                                                                                                                                                                                  |
|      |               |                                                                                                                                                                                                                                                                      |
|      |               | T-tests, ANOVA                                                                                                                                                                                                                                                       |
+------+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 5    | 9/18          | Before class: [Iterate](https://posit.cloud/learn/primers/5)                                                                                                                                                                                                         |
|      |               |                                                                                                                                                                                                                                                                      |
|      |               | Linear modelling pt. 1                                                                                                                                                                                                                                               |
+------+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 6    | 9/25          | Before class: [Write Functions](https://posit.cloud/learn/primers/6)                                                                                                                                                                                                 |
|      |               |                                                                                                                                                                                                                                                                      |
|      |               | Linear modelling pt. 2                                                                                                                                                                                                                                               |
+------+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 7    | 10/2          | Modelling assumptions, power                                                                                                                                                                                                                                         |
+------+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 8    | 10/9          | PCA                                                                                                                                                                                                                                                                  |
+------+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

## Additional introductory resources {.unnumbered}

If you are looking to learn even more outside of what this class offers, below are some great introductory R resources:

-   [Stat 158](https://csu-r.github.io/Module1/) - Vectors, data frames, installing R, etc...

-   [RStudio Materials](https://education.rstudio.com/learn/beginner/) - A series of videos, books, and more to get you started in R.

#### Tidyverse Introduction

-   [R for Data Science](https://r4ds.had.co.nz/introduction.html) - Covers all of the basic intro material, from a tidyverse perspective. As discussed, this is one way to find solutions in R, it happens to be my preferred way, but there are lots of Base R ways that work just fine!

-   [Stat 159](https://csu-r.github.io/Module2/) - A CSU specific course for an intro to the tidyverse

-   [R Markdown](https://bookdown.org/yihui/rmarkdown/#preface) - The primary book for learning more about R Markdown and all of its quirks.

-   [Cheatsheets](https://www.rstudio.com/resources/cheatsheets/) - Short, clear documents that cover so much material from dplyr to shiny apps. Great for quick references. We find the [`rmarkdown`](https://rstudio.github.io/cheatsheets/html/rmarkdown.html?_gl=1*1f2w4s3*_ga*MTc5NTY0NDA0Mi4xNjg2MzQ0MDUy*_ga_2C0WZ1JHG0*MTY5MTk1OTY1Ni42LjAuMTY5MTk1OTY1Ni4wLjAuMA..) and [`ggplot2`](https://rstudio.github.io/cheatsheets/html/data-visualization.html?_gl=1*1f2w4s3*_ga*MTc5NTY0NDA0Mi4xNjg2MzQ0MDUy*_ga_2C0WZ1JHG0*MTY5MTk1OTY1Ni42LjAuMTY5MTk1OTY1Ni4wLjAuMA..) ones particularly useful!
