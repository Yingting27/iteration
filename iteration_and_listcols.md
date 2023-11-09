Iteration and listcols
================

Load key packages.

``` r
library(tidyverse)
library(rvest)
```

    ## 
    ## Attaching package: 'rvest'

    ## The following object is masked from 'package:readr':
    ## 
    ##     guess_encoding

Set seed for reproducibility.

``` r
set.seed(12345)
#This ensures that if you run a piece of code that involves random numbers, you'll get the same results each time you run it, making your code reproducible
```

``` r
vec_numeric=1:4
vec_char=c("my", "name","is","Yingting")

tibble(
  num=vec_numeric,
  char=vec_char
)
```

    ## # A tibble: 4 × 2
    ##     num char    
    ##   <int> <chr>   
    ## 1     1 my      
    ## 2     2 name    
    ## 3     3 is      
    ## 4     4 Yingting

Different stuff with different lengths

``` r
l = 
  list(
  vec_numeric = 1:5,
  vec_char = LETTERS,
  matrix = matrix(1:10, nrow = 5, ncol=2),
  summary = summary(rnorm(100))
  )
```

Accessing lists

``` r
l$vec_char
```

    ##  [1] "A" "B" "C" "D" "E" "F" "G" "H" "I" "J" "K" "L" "M" "N" "O" "P" "Q" "R" "S"
    ## [20] "T" "U" "V" "W" "X" "Y" "Z"

``` r
l[[2]]
```

    ##  [1] "A" "B" "C" "D" "E" "F" "G" "H" "I" "J" "K" "L" "M" "N" "O" "P" "Q" "R" "S"
    ## [20] "T" "U" "V" "W" "X" "Y" "Z"

``` r
l[["summary"]]
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ## -2.3804 -0.5901  0.4837  0.2452  0.9004  2.4771

``` r
# $access name things on the list
#the [[]] would take the specific part in the list, for example, the [[2]] would be var_char as it is second one
```

### loops

``` r
list_norm_samples = 
  list(
    a = rnorm(20,1,5),
    b = rnorm(20,0,7),
    c = rnorm(20,20,1),
    d = rnorm(20,-45,13)
  )
```

mean and sd functions

``` r
mean_and_sd = function(x) {
  
  if (!is.numeric(x)) {
    stop("Argument should be numbers")
  } else if (length(x) < 2) {
    stop("You need at least 2 numbers to get z scores")
  }

  mean_x = mean(x)
  sd_x = sd(x)
  
  tibble(
    mean = mean_x,
    sd = sd_x
  )
  
}
```

``` r
mean_and_sd(list_norm_samples$a)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  1.25  4.92

``` r
mean_and_sd(list_norm_samples$b)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 0.690  9.30

``` r
mean_and_sd(list_norm_samples$c)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  19.8 0.910

``` r
mean_and_sd(list_norm_samples$d)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -44.1  14.0

``` r
# Initialize the output list
output = vector("list", length = 4)

# Loop through the list_norm_samples
for(i in 1:4) {
  
  output[[i]]=mean_and_sd(list_norm_samples[[i]])
}
```

### use `map`

``` r
output = map(list_norm_samples, mean_and_sd)
# the first one would be list of input, the second is function that apply

output = map(list_norm_samples, median)

output = map(list_norm_samples, summary)
```
