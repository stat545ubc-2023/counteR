
<!-- README.md is generated from README.Rmd. Please edit that file -->

# counteR

<!-- badges: start -->
<!-- badges: end -->

The counteR contains only one function named
`count_all_missing_by_group`. It is named `counteR` since the package
can be expanded in the future in a way that provides general-purpose
counting functions for data tables. For now, the goal of counteR is to
group the given data table and count the missing (`NA`) values on the
columns that are not `group` for each of the grouping results, according
to the given group column(s). It creates a new table for that purpose
and returns it.

## Installation

You can install the development version of counteR from
[GitHub](https://github.com/) with using the following lines on your R
terminal or files:

``` r
# install.packages("devtools")
devtools::install_github("stat545ubc-2023/counteR")
#> Downloading GitHub repo stat545ubc-2023/counteR@HEAD
#> rlang     (1.1.1 -> 1.1.2) [CRAN]
#> lifecycle (1.0.3 -> 1.0.4) [CRAN]
#> withr     (2.5.0 -> 2.5.2) [CRAN]
#> vctrs     (0.6.3 -> 0.6.4) [CRAN]
#> utf8      (1.2.3 -> 1.2.4) [CRAN]
#> fansi     (1.0.4 -> 1.0.5) [CRAN]
#> Installing 6 packages: rlang, lifecycle, withr, vctrs, utf8, fansi
#> Installing packages into '/private/var/folders/dy/5gjrhf8j29j9pz5tk6gwp3rr0000gn/T/RtmpWJnK69/temp_libpath7cf25ee78fae'
#> (as 'lib' is unspecified)
#> 
#> The downloaded binary packages are in
#>  /var/folders/dy/5gjrhf8j29j9pz5tk6gwp3rr0000gn/T//RtmpKBCOL0/downloaded_packages
#> ── R CMD build ─────────────────────────────────────────────────────────────────
#> * checking for file ‘/private/var/folders/dy/5gjrhf8j29j9pz5tk6gwp3rr0000gn/T/RtmpKBCOL0/remotes7d7f60f2b680/stat545ubc-2023-counteR-e618f16/DESCRIPTION’ ... OK
#> * preparing ‘counteR’:
#> * checking DESCRIPTION meta-information ... OK
#> * checking for LF line-endings in source and make files and shell scripts
#> * checking for empty or unneeded directories
#> * building ‘counteR_0.1.0.tar.gz’
#> Installing package into '/private/var/folders/dy/5gjrhf8j29j9pz5tk6gwp3rr0000gn/T/RtmpWJnK69/temp_libpath7cf25ee78fae'
#> (as 'lib' is unspecified)
```

## Syntax and Parameters:

    count_all_missing_by_group(data, group_col, .groups="drop")

- data: the dataset you would use for the missing value counting
- group_col: the column(s) that the grouping will be performed on
- .groups: resulted data table’s grouping condition, it follows the
  [`dplyr::summarize`](https://dplyr.tidyverse.org/reference/summarise.html)
  function’s usage.

One can use `?count_all_missing_by_group` line in the R terminal to see
the further documentation.

## Examples

This is how you can count the missing values on each of the columns
despite the `group_col` of the specified column’s groups with using
`counteR`‘s `count_all_missing_by_group` function (see the output
tables’ first few lines):

``` r
library(counteR)
# install.packages("datateachr")
library(datateachr) # for using the datasets

## basic example code
count_all_missing_by_group(steam_games, types) # according to the column type's groups, drops the groupings as it is the default behavior, you can use .groups = "drop" in order to do the same thing
#> # A tibble: 4 × 21
#>   types     id   url  name desc_snippet recent_reviews all_reviews release_date
#>   <chr>  <int> <int> <int>        <int>          <int>       <int>        <int>
#> 1 app        0     0     0           39          35315        9551            0
#> 2 bundle     0     0     0            0              0           0            0
#> 3 sub        0     0     0            0              0           0            0
#> 4 <NA>       0     0     2            2              2           2            2
#> # ℹ 13 more variables: developer <int>, publisher <int>, popular_tags <int>,
#> #   game_details <int>, languages <int>, achievements <int>, genre <int>,
#> #   game_description <int>, mature_content <int>, minimum_requirements <int>,
#> #   recommended_requirements <int>, original_price <int>, discount_price <int>
count_all_missing_by_group(steam_games, types, "keep") # according to the column type's groups, keeps the groupings on the table
#> # A tibble: 4 × 21
#> # Groups:   types [4]
#>   types     id   url  name desc_snippet recent_reviews all_reviews release_date
#>   <chr>  <int> <int> <int>        <int>          <int>       <int>        <int>
#> 1 app        0     0     0           39          35315        9551            0
#> 2 bundle     0     0     0            0              0           0            0
#> 3 sub        0     0     0            0              0           0            0
#> 4 <NA>       0     0     2            2              2           2            2
#> # ℹ 13 more variables: developer <int>, publisher <int>, popular_tags <int>,
#> #   game_details <int>, languages <int>, achievements <int>, genre <int>,
#> #   game_description <int>, mature_content <int>, minimum_requirements <int>,
#> #   recommended_requirements <int>, original_price <int>, discount_price <int>
count_all_missing_by_group(chickwts, feed, "rowwise")
#> # A tibble: 6 × 2
#> # Rowwise:  feed
#>   feed      weight
#>   <fct>      <int>
#> 1 casein         0
#> 2 horsebean      0
#> 3 linseed        0
#> 4 meatmeal       0
#> 5 soybean        0
#> 6 sunflower      0
```

## Developer

This package is developed using the conventions of [R Packages
(2e)](https://r-pkgs.org) for the library structure. It is recommended
to use the same conventions described by following links in order to
contribute to this open-source package.

1.  Testing: <https://r-pkgs.org/testing-basics.html>
2.  R Code: <https://r-pkgs.org/code.html>
3.  Description: <https://r-pkgs.org/description.html>
4.  Licensing: <https://r-pkgs.org/license.html>
5.  Function documentation: <https://r-pkgs.org/man.html>
6.  Readme: <https://r-pkgs.org/other-markdown.html>
