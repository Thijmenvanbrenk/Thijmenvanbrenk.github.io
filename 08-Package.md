---
title: "SQL"
author: "Thijmen"
output: bookdown::html_document2
---

## Creating a package

Creating a package can save people allot of time, because they don't have to write the same piece of code multiple times.        
That is why having the ability to make a package is very important as a data scientist.       
<br>        
Because I am obsessed with bees I decided to make my life a bit easier, that's why I created a package that will perform my calculations for me so I can save myself some time and make my life just that extra bit easier.       
[You can find this package by clicking this link.](https://github.com/thijmenvanbrenk/beecalculator)       

You can download the package by using these two lines.

`install.packages("devtools")`       
`devtools::install_github("thijmenvanbrenk/beecalculator")`

By using `help(package = "beecalculator")` you will get a nice overview of the available data and functions available in this package.        
To get a detailed description of what everything does use `browseVignettes("beecalculator")` to see all the possibilities with this package.
