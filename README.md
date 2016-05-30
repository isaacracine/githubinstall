# An Easy Way to Install R Packages on GitHub
Koji MAKIYAMA (@hoxo_m)  



[![Travis-CI Build Status](https://travis-ci.org/hoxo-m/githubinstall.svg?branch=master)](https://travis-ci.org/hoxo-m/githubinstall)
[![CRAN Version](http://www.r-pkg.org/badges/version/githubinstall)](http://cran.rstudio.com/web/packages/githubinstall)
[![Coverage Status](https://coveralls.io/repos/github/hoxo-m/githubinstall/badge.svg?branch=master)](https://coveralls.io/github/hoxo-m/githubinstall?branch=master)

## 1. Overview

A growing number of R packages are created by various people in the world.
A part of the cause of it is the **devtools** package that makes it easy to develop R packages.
The **devtools** package not only facilitates the process to develop R packages but also provides the another way to distribute R packages.

To distribute R packages, the CRAN is commonly used.
You can install the packages are available on CRAN as follows.


```r
install.packages("dplyr")
```

The **devtools** package provides `install_github()` that enables installing packages on GitHub.


```r
library(devtools)
install_github("hadley/dplyr")
```

Therefore, developers can distribute R packages that is developing on GitHub.
There are some developers who have no intention to submit to CRAN.
For example, Twitter, Inc. provides **AnomalyDetection** package on GitHub but it is not available on CRAN.[^1] You can install such packages easily by using **devtools**.


```r
library(devtools)
install_github("twitter/AnomalyDetection")
```

[^1]:[Introducing practical and robust anomaly detection in a time series](https://blog.twitter.com/2015/introducing-practical-and-robust-anomaly-detection-in-a-time-series)

There is a difference what is passed between `install.packages()` and `install_github()`.
`install.packages()` takes the package names and `install_github()` needs the repositry names.
It means that if you want to install a package on GitHub you must remember its repository name exactly.

The trouble is that the usernames of GitHub are often hard to remember.
For instance, **ggfortify** is a great package on GitHub but who created it?
What is the username? 
The answer is [sinhrks](https://github.com/sinhrks/ggfortify).
I think it is difficult to remember the name.

The **githubinstall** package provides a way to install packages on GitHub by the only package names just like `isntall.packages()`.


```r
library(githubinstall)
githubinstall("AnomalyDetection")
```

And furthermore, you may succeed in installing packages with vague package names.


```r
githubinstall("anomaly detection")
```

## 2. Installation

You can install the package from GitHub.


```r
install.packages("devtools") # if you have not installed "devtools" package
devtools::install_github("hoxo-m/githubinstall")
```

The source code for **githubinstall** package is available on GitHub at

- https://github.com/hoxo-m/githubinstall.

## 3. Details

This package completes `username` automatically.


```r
library(githubinstall)
```


```r
githubinstall("AnomalyDetection")
# This is same as devtools::install_github("twitter/AnomalyDetection")
```

Or


```r
gh_install_packages("AnomalyDetection", build_vignettes = F)
```

```
Downloading GitHub repo hadley/multidplyr@master
Installing multidplyr
...
* DONE (multidplyr)
```

You can show the list of repositories on GitHub by `username`.


```r
hadleyverse <-  gh_get_package_info("hadley")
head(hadleyverse)
```

```
##   author package_name
## 1 hadley   assertthat
## 2 hadley    babynames
## 3 hadley    bigrquery
## 4 hadley     bookdown
## 5 hadley   clusterfly
## 6 hadley      decumar
##                                                                 title
## 1                                      User friendly assertions for R
## 2               An R package contain all baby names data from the SSA
## 3                           An interface to Google's bigquery from R.
## 4                                                               Watch
## 5 An R package for visualising high-dimensional clustering algorithms
## 6                                            An alternative to sweave
```

You can guess repository names or user names.


```r
gh_guess_username("hadly")
```

```
## [1] "hadley"
```

## 4. Related Work

- devtools: [Tools to make an R developer's life easier](https://github.com/hadley/devtools)
- ghit: [Lightweight GitHub Package Installer](https://github.com/cloudyr/ghit)
- drat: [Drat R Archive Template](https://github.com/eddelbuettel/drat)
- pacman: [A package management tools for R](https://github.com/trinker/pacman)
- remotes: [Install R packages from GitHub, Bitbucket, git, svn repositories, URLs](https://github.com/MangoTheCat/remotes)
