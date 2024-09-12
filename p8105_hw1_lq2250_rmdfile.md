p8105_hw1_lq2250
================
Lanlan_Qing
2024-09-12

# This is a Rmarkdown file of Homework1

## Data of penguins package

### Loading data

``` r
data("penguins", package = "palmerpenguins")
```

### Extract information

``` r
num_row = nrow(penguins)
num_col = ncol(penguins)
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ ggplot2   3.5.1     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.3     ✔ tidyr     1.3.1
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
mean_flipper_len = format(round(mean(pull(penguins, flipper_length_mm), na.rm = TRUE),2))
```

### Results

The **size** of the the dataset is **344** rows and **8** columns.<br>
The **mean flipper length** is **200.92**mm.

## The scatterplot of flipper length(mm) v.s bill length(mm)

``` r
library(ggplot2)
ggplot(penguins, 
       aes(x = bill_length_mm, y = flipper_length_mm ))+
  geom_point(aes(color = species))
```

    ## Warning: Removed 2 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](p8105_hw1_lq2250_rmdfile_files/figure-gfm/scatterplot_flip_vs_bill-1.png)<!-- -->

``` r
ggsave('scatterplot_flipper_vs_bill.pdf')
```

    ## Saving 7 x 5 in image

    ## Warning: Removed 2 rows containing missing values or values outside the scale range
    ## (`geom_point()`).
