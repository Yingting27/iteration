writing_functions
================
Yingting Zhang
2023-11-08

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.3     ✔ readr     2.1.4
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.0
    ## ✔ ggplot2   3.4.3     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(rvest)
```

    ## 
    ## Attaching package: 'rvest'
    ## 
    ## The following object is masked from 'package:readr':
    ## 
    ##     guess_encoding

Set seed for reproducibility

``` r
set.seed(12345)
# when pick random number, you can specific one, use set seed to get the same random number
```

### Z score function

Z scores subtract the mean and divide by the sd.

``` r
x_vec = rnorm(20, mean = 5, sd = .3)
```

compute Z scores for ‘x_vec’.

``` r
(x_vec - mean(x_vec)) / sd(x_vec)
```

    ##  [1]  0.6103734  0.7589907 -0.2228232 -0.6355576  0.6347861 -2.2717259
    ##  [7]  0.6638185 -0.4229355 -0.4324994 -1.1941438 -0.2311505  2.0874460
    ## [13]  0.3526784  0.5320552 -0.9917420  0.8878182 -1.1546150 -0.4893597
    ## [19]  1.2521303  0.2664557

write a function to do this!

``` r
z_score = function(x) {
  
  if(!is.numeric(x)){
    stop("Argument should be numbers")
  } else if (length(x) < 2){
    stop("You need at least 2 numbers to get z scores")
  }
  
  z = (x-mean(x)) / sd(x)
  
  z
}
```

check that this works

``` r
z_score(x = x_vec)
```

    ##  [1]  0.6103734  0.7589907 -0.2228232 -0.6355576  0.6347861 -2.2717259
    ##  [7]  0.6638185 -0.4229355 -0.4324994 -1.1941438 -0.2311505  2.0874460
    ## [13]  0.3526784  0.5320552 -0.9917420  0.8878182 -1.1546150 -0.4893597
    ## [19]  1.2521303  0.2664557

``` r
z_score(x = rnorm(10, mean = 5))
```

    ##  [1]  0.5952213  1.1732833 -0.6221352 -1.3990896 -1.4371950  1.4719158
    ##  [7] -0.4830567  0.4590828  0.4520244 -0.2100512

keep checking

``` r
z_score(x=3)
```

    ## Error in z_score(x = 3): You need at least 2 numbers to get z scores

``` r
z_score(c("my","name","is","Yingting"))
```

    ## Error in z_score(c("my", "name", "is", "Yingting")): Argument should be numbers

``` r
z_score(c(TRUE, TRUE, FALSE, FALSE))
```

    ## Error in z_score(c(TRUE, TRUE, FALSE, FALSE)): Argument should be numbers

``` r
z_score(iris)
```

    ## Error in z_score(iris): Argument should be numbers

### multiple outputs

write a function that returns the mean and sd from a sample of numbers

``` r
mean_and_sd = function(x) {
    if(!is.numeric(x)){
    stop("Argument should be numbers")
  } else if (length(x) < 2){
    stop("You need at least 2 numbers to get z scores")
  }
  mean_x = mean(x)
  sd_x=sd(x)
  
  tibble(
    mean=mean_x,
    sd=sd_x
  )
}
```

double chekc i did this right..

``` r
mean_and_sd(x_vec)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  5.02 0.250

### start getting means and sds

``` r
x_vec = rnorm(n= 30, mean=5,sd=.5)
  tibble(
    mean=mean(x_vec),
    sd=sd(x_vec)
  )
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  5.16 0.643

let’s write a function that uses `n`, a true mean, and true SD as inputs

``` r
sim_mean_sd = function(n_obs, mu, sigma){
  
  
x_vec = rnorm(n= n_obs, mean=mu,sd=sigma)

  tibble(
    mean=mean(x_vec),
    sd=sd(x_vec)
  )
}

sim_mean_sd(n_obs = 30, mu=5, sigma=.5)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  5.22 0.543

``` r
sim_mean_sd(12,24,4)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  23.6  4.49