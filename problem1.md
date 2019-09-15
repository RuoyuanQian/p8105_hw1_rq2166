p8105\_hw1\_rq2166
================
Ruoyuan Qian
2019/9/14

# Problem 1

\`\`\`{r create data frame,eval = FALSE,warning = FALSE}
library(tidyverse) df \<- tibble( ran=rnorm(8), logic= ran\>0, char=
c(“I”, “l”, “o”, “v”,“e”, “d”,“s”,“\!”),
fact=factor(c(rep(1,3),rep(2,4),rep(3,1))))

\#calculate means mean(df\(ran) mean(df\)logic)
mean(df\(char) mean(df\)fact)

\#define as numeric as.numeric(df\(logic) as.numeric(df\)char)
as.numeric(df$fact)

\`\`\`

In problem one, When I try to take the mean of each variable, the
logical vector and random vector work, but the charater vector and the
factor vector display errors and get “NA” results.

When I use `as.numeric()` function to change the them into numeric
vectors, the logical vector and factor vector work, but sill displaying
error in charactor vector.

It dose explain the failure in calculating the mean in charactor and
factor vectors, since they are initially defined as charactors, which is
impossible to determine the means. That’s why there are errors in them.
