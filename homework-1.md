p8105\_hw1\_rq2166
================
Ruoyuan Qian
2019/9/19

# Problem 1

create data
    frame

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 3.2.1     ✔ purrr   0.3.2
    ## ✔ tibble  2.1.3     ✔ dplyr   0.8.3
    ## ✔ tidyr   1.0.0     ✔ stringr 1.4.0
    ## ✔ readr   1.3.1     ✔ forcats 0.4.0

    ## ── Conflicts ────────────────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
library(ggplot2)
set.seed(961223)

df <- tibble( ran  = rnorm(8),
              logic= ran > 0 ,
              char = c("I", "l", "o", "v",
                       "e", "d","s","!"),
              fact = factor(c(rep(1,3),
                              rep(2,4),
                              rep(3,1))))

#calculate means
pull(df,ran) %>% 
mean()
```

    ## [1] -0.382586

``` r
pull(df,logic) %>% 
mean()
```

    ## [1] 0.375

``` r
pull(df,char) %>% 
mean()
```

    ## Warning in mean.default(.): argument is not numeric or logical: returning
    ## NA

    ## [1] NA

``` r
pull(df,fact) %>% 
mean()
```

    ## Warning in mean.default(.): argument is not numeric or logical: returning
    ## NA

    ## [1] NA

define as numeric

``` r
pull(df,logic) %>% 
as.numeric()

pull(df,char) %>% 
as.numeric()


pull(df,fact) %>% 
as.numeric()
```

In problem one, when I try to take the mean of each variable, the
logical vector and random vector work, but the charater vector and the
factor vector display warnings and get “NA” results.

When I use `as.numeric()` function to change the them into numeric
vectors, the logical vector and factor vector work, but sill displaying
warnings in charactor vector. Since factor vector saves its contet as
numbers based on different levels, as a reslut, it can be changed as
numeric one.

It dose explain the failure in calculating the mean in charactor and
factor vectors, since they are initially defined as charactors, which is
impossible to determine the means. That’s why there are warnings and
“NA”s in them.

logical vector converting

``` r
#covert logical vector to numric vetor 

 pull(df,logic) %>% 
 as.numeric() *  pull(df,ran)
```

    ## [1] 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.9743737 0.2975352
    ## [8] 0.8974512

``` r
#covert logical vector to factor vetor 
 
 pull(df,logic) %>% 
 as.factor() *  pull(df,ran)
```

    ## Warning in Ops.factor(pull(df, logic) %>% as.factor(), pull(df, ran)): '*'
    ## not meaningful for factors

    ## [1] NA NA NA NA NA NA NA NA

``` r
#covert logical vector to factor and then convert result
  pull(df,logic) %>% 
  as.factor() %>% 
  as.numeric() * pull(df,ran)
```

    ## [1] -0.3874046 -0.2157536 -0.9511222 -2.0642095 -1.6115586  1.9487473
    ## [7]  0.5950704  1.7949024

# Problem 2

create data frame and make description

``` r
df2 <- tibble(x = rnorm(500),
              y = rnorm(500),
              logic = x + y > 1,
              nume  = as.numeric(logic),
              fac   = as.factor (logic))


x_sum <- tibble( nrow = nrow(df2),
                 ncol = ncol(df2),
                 x_mean   = mean(df2$x),
                 x_median = median(df2$x),
                 x_SD     = sd(df2$x) )


pull(df2,logic) %>%
table() %>% 
prop.table() 
```

    ## .
    ## FALSE  TRUE 
    ## 0.738 0.262

``` r
x_sum
```

    ## # A tibble: 1 x 5
    ##    nrow  ncol x_mean x_median  x_SD
    ##   <int> <int>  <dbl>    <dbl> <dbl>
    ## 1   500     5 0.0662   0.0564  1.00

draw plots

``` r
 ggplot( df2, aes(x, y, color = logic)) + 
  geom_point(size = 1.0, shape = 16)    + 
  labs(  title = "scatterplot of y vs x",
         x     = "x",
         y     = "y")
```

![](homework-1_files/figure-gfm/Problem%202%20draw%20plot-1.png)<!-- -->

``` r
 ggplot( df2, aes(x, y, color = nume)) +
  geom_point(size = 1.0, shape = 16)   +
  labs(  title    = "scatterplot of y vs x",
         x        = "x",
         y        = "y")
```

![](homework-1_files/figure-gfm/Problem%202%20draw%20plot-2.png)<!-- -->

``` r
 ggplot( df2, aes(x, y,color = fac)) + 
  geom_point(size = 1.0, shape = 16) +
  labs(  title    = "scatterplot of y vs x",
         x        = "x",
         y        = "y")
```

![](homework-1_files/figure-gfm/Problem%202%20draw%20plot-3.png)<!-- -->

save plot 1

``` r
plot_1 <- 
  ggplot(df2, 
         aes(x, y, color = logic)) + 
  geom_point(size = 1.0)           + 
  labs(title= "scatterplot of y vs x",
       x    = "x",
       y    = "y")

ggsave("plot_1.pdf")
```

    ## Saving 7 x 5 in image

The color of scales are different based on the different types of
variables in `color=`function.

As for the logical variable, the scale contains just two groups, `TRUE`
and `FALSE`.

As for the numeric variable, the scale is continuous from `0` to `1`.

As for the logical variable, the scale contains just two groups, `TRUE`
and `FALSE`, which is same as the first one.
