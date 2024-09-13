p8105_hw1_lq2250
================
Lanlan_Qing
2024-09-12

# This is a Rmarkdown file of Homework1

## Problem 1

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

The *size* of the the dataset is **344** rows and **8** columns.<br> The
*mean flipper length* is **200.92**mm.

### The scatterplot of flipper length(mm) v.s bill length(mm)

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

## Problem 2

### Create the dataframe

``` r
norm_sample = rnorm(10)
cha_vec = c('Red','Yellow','Red','White','Red','Yellow','Yellow','White','White','White')
log_vec = c(norm_sample > 0)
fac_vec = factor(cha_vec, nmax = 3)
data_frame = data.frame(norm_sample,
                        log_vec,
                        cha_vec,
                        fac_vec)
```

### Take the mean of each variable

``` r
num_mean = mean(pull(data_frame, norm_sample))
log_mean = mean(pull(data_frame, log_vec))
cha_mean = mean(pull(data_frame, cha_vec))
```

    ## Warning in mean.default(pull(data_frame, cha_vec)): argument is not numeric or
    ## logical: returning NA

``` r
fac_mean = mean(pull(data_frame, fac_vec))
```

    ## Warning in mean.default(pull(data_frame, fac_vec)): argument is not numeric or
    ## logical: returning NA

### Results

The mean of *random sample* is **0.3912084**.<br> The mean of *logical
vector* is **0.5**.<br> The mean of *character vector* is **NA**.<br>
The mean of *factor vector* is **NA**.<br>

**Q: Try to take the mean of each variable in your dataframe. What works
and what doesn’t?** <br> The mean of a **numeric vector** like sample
can directly return a valid result. <br> The **logical vector** should
return a result of NA, but it has internal numeric value where “TRUE”
returns to 1 and “FALSE” returns to 0, so there’s still numeric mean
calculated.<br> **Character** and **factor vectors** are composed of
non-numeric elements, which are not applicable for mean calculation.

### Application of numeric function

``` r
log_mean_num = as.numeric(log_mean)
cha_mean_num = as.numeric(cha_mean)
fac_mean_num = as.numeric(fac_mean)
```

**Q: What happens, and why? Does this help explain what happens when you
try to take the mean?** <br> **Logical**: TRUE becomes 1 and FALSE
becomes 0.<br> **Character**: Results in NA with a warning, as
non-numeric characters can’t be directly converted to numeric. <br>
**Factor**: The function converts factors to their internal numeric
levels.
