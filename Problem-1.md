p8105\_hw1\_rq2166
================
Ruoyuan Qian
2019/9/14

# Problem 1

\#\#create data
    frame

``` r
library(tidyverse)
```

    ## ── Attaching packages ───────────────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 3.2.1     ✔ purrr   0.3.2
    ## ✔ tibble  2.1.3     ✔ dplyr   0.8.3
    ## ✔ tidyr   1.0.0     ✔ stringr 1.4.0
    ## ✔ readr   1.3.1     ✔ forcats 0.4.0

    ## ── Conflicts ──────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
df <- tibble( ran=rnorm(8),
              logic= ran>0,
              char= c("I", "l", "o", 
                             "v","e", "d","s","!"),
              fact=factor(c(rep(1,3),rep(2,4),rep(3,1))))

#calculate means
mean(df$ran)
```

    ## [1] -0.8021678

``` r
mean(df$logic)
```

    ## [1] 0.25

``` r
mean(df$char)
```

    ## Warning in mean.default(df$char): argument is not numeric or logical:
    ## returning NA

    ## [1] NA

``` r
mean(df$fact)
```

    ## Warning in mean.default(df$fact): argument is not numeric or logical:
    ## returning NA

    ## [1] NA

\#\#define as numeric

``` r
as.numeric(df$logic)
as.numeric(df$char)
as.numeric(df$fact)
```

In problem one, When I try to take the mean of each variable, the
logical vector and random vector work, but the charater vector and the
factor vector display warnings and get “NA” results.

When I use `as.numeric()` function to change the them into numeric
vectors, the logical vector and factor vector work, but sill displaying
warnings in charactor vector.

It dose explain the failure in calculating the mean in charactor and
factor vectors, since they are initially defined as charactors, which is
impossible to determine the means. That’s why there are warnings and
“NA”s in them.

\#\#logical vector converting

``` r
#covert logical vector to numric vetor 
logic_numeric <- as.numeric(df$logic)
 logic_numeric * df$ran
```

    ## [1] 0.0000000 0.0000000 0.2438743 0.0000000 0.0000000 1.1018142 0.0000000
    ## [8] 0.0000000

``` r
#covert logical vector to factor vetor 
logic_fact <- as.factor(df$logic)
 logic_fact * df$ran
```

    ## Warning in Ops.factor(logic_fact, df$ran): '*' not meaningful for factors

    ## [1] NA NA NA NA NA NA NA NA

``` r
#covert logical vector to factor and then convert result
logic_fact <- as.factor(df$logic)
fact_num <- as.numeric(logic_fact )
 fact_num*df$ran
```

    ## [1] -0.9957844 -1.5941172  0.4877486 -0.7106040 -0.1207970  2.2036284
    ## [7] -0.6423746 -3.6993538

# Problem 2

\#\#create data frame and make description

``` r
library(tidyverse)

df2<-tibble(x=rnorm(500),
            y=rnorm(500),
            logic= x+y>1,
            nume=as.numeric(logic),
            fac=as.factor(logic))


x_sum <- tibble( nrow=nrow(df2),
                 ncol=ncol(df2),
                 x_mean=mean(df2$x),
                 x_median=median(df2$x),
                 x_SD=sd(df2$x) )
x_sum
```

    ## # A tibble: 1 x 5
    ##    nrow  ncol x_mean x_median  x_SD
    ##   <int> <int>  <dbl>    <dbl> <dbl>
    ## 1   500     5 -0.115  -0.0657  1.02

``` r
prop.table(table(df2$logic))
```

    ## 
    ## FALSE  TRUE 
    ## 0.764 0.236

\#\#draw plots

``` r
library(ggplot2)

ggplot(df2, aes(x, y,color= df2$logic))+geom_point(size = 1.0)+ labs(title="scatterplot of y vs x",x="x",y="y")
```

![](Problem-1_files/figure-gfm/Problem%202%20draw%20plot-1.png)<!-- -->

``` r
ggplot(df2, aes(x, y,color= df2$nume))+geom_point(size = 1.0, shape = 16)+
  labs(title="scatterplot of y vs x",x="x",y="y")
```

![](Problem-1_files/figure-gfm/Problem%202%20draw%20plot-2.png)<!-- -->

``` r
ggplot(df2, aes(x, y,color= df2$fac))+geom_point(size = 1.0, shape = 16)+
  labs(title="scatterplot of y vs x",x="x",y="y")
```

![](Problem-1_files/figure-gfm/Problem%202%20draw%20plot-3.png)<!-- -->

\#save plot
1

``` r
plot_1 <- ggplot(df2, aes(x, y,color= df2$logic))+geom_point(size = 1.0)+ labs(title="scatterplot of y vs x",x="x",y="y")
ggsave("plot_1.pdf")
```

    ## Saving 7 x 5 in image

The color scales are different based on the different types of variables
in `color=`function.

As for the logical variable, the scale contains just two groups, TRUE
and FALSE.

As for the numeric variable, the scale is a continuous vector from `0`
to `1`, TRUE and FALSE.

As for the logical variable, the scale contains just two groups, TRUE
and FALSE, which is same as the first one.
