Lab 02 - Plastic waste
================
Rachel Good
01/11/2022

## Load packages and data

``` r
library(tidyverse) 
```

``` r
plastic_waste <- read.csv("data/plastic-waste.csv")
```

## Exercises

### Exercise 1

Trinidad and Tobago is a extreme outlier as the carribean islands are
one of the world’s leading producers of plastic waste.

``` r
ggplot(data = plastic_waste, aes(x = plastic_waste_per_cap)) +
  geom_histogram(binwidth = 0.2)
```

    ## Warning: Removed 51 rows containing non-finite values (stat_bin).

![](lab-02_files/figure-gfm/plastic-waste-continent-1.png)<!-- -->

``` r
plastic_waste %>%
  filter(plastic_waste_per_cap > 3.5)
```

    ##   code              entity     continent year gdp_per_cap plastic_waste_per_cap
    ## 1  TTO Trinidad and Tobago North America 2010    31260.91                   3.6
    ##   mismanaged_plastic_waste_per_cap mismanaged_plastic_waste coastal_pop
    ## 1                             0.19                    94066     1358433
    ##   total_pop
    ## 1   1341465

``` r
ggplot(data = plastic_waste, 
       mapping = aes(x = plastic_waste_per_cap, 
                     color = continent,
                     fill = continent)) +
  geom_density(alpha = 0.7)
```

    ## Warning: Removed 51 rows containing non-finite values (stat_density).

![](lab-02_files/figure-gfm/density%20plot-1.png)<!-- -->

### Exercise 2

``` r
ggplot(data = plastic_waste, 
       mapping = aes(x = plastic_waste_per_cap, 
                     color = continent,
                     fill = continent)) +
  geom_density(alpha = 0.3)
```

    ## Warning: Removed 51 rows containing non-finite values (stat_density).

![](lab-02_files/figure-gfm/plastic-waste-density-1.png)<!-- -->

We define color and fill by the mapping aesthetics because we need to
assign those qualities to specific variables. On the otherhand, alpha
applies to the entire visual and does not need to be changed based on a
variable level.

### Exercise 3

``` r
ggplot(data = plastic_waste, 
       mapping = aes(x = continent, 
                     y = plastic_waste_per_cap)) +
  geom_boxplot()
```

    ## Warning: Removed 51 rows containing non-finite values (stat_boxplot).

![](lab-02_files/figure-gfm/boxplot-1.png)<!-- -->

### Exercise 4

``` r
ggplot(data = plastic_waste, 
       mapping = aes(x = continent,
                     y = plastic_waste_per_cap,)) +
  geom_violin()
```

    ## Warning: Removed 51 rows containing non-finite values (stat_ydensity).

![](lab-02_files/figure-gfm/violin%20plot-1.png)<!-- -->

The violin plot more clearly displays the density plot for each
continent than the density plot shown above. Unlike the boxplot, the
violin plot does not clearly show the quartiles, nor the mean of the
data set. It also does not have clear points for outliers in the data.

### Exercise 5

Remove this text, and add your answer for Exercise 5 here.

``` r
ggplot(data = plastic_waste, 
       mapping = aes(x = plastic_waste_per_cap,
                     y = mismanaged_plastic_waste_per_cap,
                     )) +
  geom_point()
```

    ## Warning: Removed 51 rows containing missing values (geom_point).

![](lab-02_files/figure-gfm/plastic-waste-mismanaged-1.png)<!-- -->

### Exercise 6

Remove this text, and add your answer for Exercise 6 here.

``` r
ggplot(data = plastic_waste, 
       mapping = aes(x = plastic_waste_per_cap,
                     y = mismanaged_plastic_waste_per_cap,
                     color = continent,
                     fill = continent)) +
  geom_point()
```

    ## Warning: Removed 51 rows containing missing values (geom_point).

![](lab-02_files/figure-gfm/plastic-waste-mismanaged-continent-1.png)<!-- -->

### Exercise 7

Remove this text, and add your answer for Exercise 7 here.

``` r
ggplot(data = plastic_waste, 
       mapping = aes(x = plastic_waste_per_cap,
                     y = total_pop,
                     color = continent,
                     fill = continent)) +
  geom_point()
```

    ## Warning: Removed 61 rows containing missing values (geom_point).

![](lab-02_files/figure-gfm/plastic-waste-population-total-1.png)<!-- -->

``` r
ggplot(data = plastic_waste, 
       mapping = aes(x = plastic_waste_per_cap,
                     y = coastal_pop,
                     color = continent,
                     fill = continent)) +
  geom_point()
```

    ## Warning: Removed 51 rows containing missing values (geom_point).

![](lab-02_files/figure-gfm/plastic-waste-population-coastal-1.png)<!-- -->

### Exercise 8

Remove this text, and add your answer for Exercise 8 here.

``` r
ggplot(data = plastic_waste)+
  geom_point(mapping = aes(x = coastal_pop/total_pop,
                     y =  plastic_waste_per_cap,
                     color = continent)) +
    geom_smooth(mapping = aes(x = coastal_pop/total_pop,
                              y = plastic_waste_per_cap))+
  ylim(0, 0.7) +
  labs(title = "Plastic waste vs. coastal population proportion",
       subtitle = "by continent",
       x = "Coastal population proportion (Coastal/total population)",
       y = "Plastic waste per capita",
       color = "Continent")
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

    ## Warning: Removed 62 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 62 rows containing missing values (geom_point).

![](lab-02_files/figure-gfm/recreate-viz-1.png)<!-- -->

## Pro-Tips

### Excercise 3

Try this :D

ggplot(data = plastic\_waste, mapping = aes(x = continent, y =
plastic\_waste\_per\_cap)) + geom\_violin()+ geom\_boxplot(width=.3,
fill=“green”) + stat\_summary(fun.y=median, geom=“point”)

### Exercise 5

Helpful
reference:<http://www.sthda.com/english/wiki/ggplot2-themes-and-background-colors-the-3-elements>
