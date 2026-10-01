01_viz
================
Emma
2026-10-01

``` r
library(tidyverse)
library(ggridges)
```

``` r
library(p8105.datasets)
data("weather_df")
```

``` r
ggplot(weather_df, aes(x = tmin, y = tmax))
```

![](01_viz_files/figure-gfm/unnamed-chunk-3-1.png)<!-- --> This creates
a blank scatterplot, no geom specified

``` r
ggplot(weather_df, aes(x = tmin, y = tmax)) + 
  geom_point()
```

    ## Warning: Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](01_viz_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

``` r
weather_df |>
  ggplot(aes(x = tmin, y = tmax)) + 
  geom_point()
```

    ## Warning: Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](01_viz_files/figure-gfm/unnamed-chunk-5-1.png)<!-- --> Better way to
write code for the same scatterplot

``` r
ggp_weather = 
  weather_df |>
  ggplot(aes(x = tmin, y = tmax)) 

ggp_weather + geom_point()
```

    ## Warning: Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](01_viz_files/figure-gfm/unnamed-chunk-6-1.png)<!-- --> Saving plot,
not Jeff’s default for making plots

# Advanced Scatterplot

``` r
weather_df |>
  ggplot(aes(x = tmin, y = tmax)) + 
  geom_point(aes(color = name))
```

    ## Warning: Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](01_viz_files/figure-gfm/unnamed-chunk-7-1.png)<!-- --> Adding color
based on name variable

``` r
weather_df |>
  ggplot(aes(x = tmin, y = tmax)) + 
  geom_point(aes(color = name), alpha = .5) +
  geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'gam' and formula = 'y ~ s(x, bs = "cs")'

    ## Warning: Removed 17 rows containing non-finite outside the scale range
    ## (`stat_smooth()`).

    ## Warning: Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](01_viz_files/figure-gfm/unnamed-chunk-8-1.png)<!-- --> Adding curve
and making dots slightly transparent

``` r
weather_df |> 
  ggplot(aes(x = tmin, y = tmax, color = name)) + 
  geom_point(alpha = .5) +
  geom_smooth(se = FALSE) + 
  facet_grid(. ~ name)
```

    ## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'

    ## Warning: Removed 17 rows containing non-finite outside the scale range
    ## (`stat_smooth()`).

    ## Warning: Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](01_viz_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

``` r
weather_df |> 
  ggplot(aes(x = date, y = tmax, color = name)) + 
  geom_point(aes(size = prcp), alpha = .5) +
  geom_smooth(se = FALSE) + 
  facet_grid(. ~ name)
```

    ## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'

    ## Warning: Removed 17 rows containing non-finite outside the scale range
    ## (`stat_smooth()`).

    ## Warning: Removed 19 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](01_viz_files/figure-gfm/unnamed-chunk-10-1.png)<!-- --> Looking at
times of year and precipitation

``` r
weather_df |>  
  ggplot(aes(x = date, y = tmax, color = name)) + 
  geom_smooth(se = FALSE) 
```

    ## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'

    ## Warning: Removed 17 rows containing non-finite outside the scale range
    ## (`stat_smooth()`).

![](01_viz_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

``` r
weather_df |> 
  ggplot(aes(x = tmax, y = tmin)) + 
  geom_hex()
```

    ## Warning: Removed 17 rows containing non-finite outside the scale range
    ## (`stat_binhex()`).

![](01_viz_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

# Learning assessment - do this

# Univariate Plots

## Histogram

``` r
weather_df |> 
  ggplot(aes(x = tmax)) + 
  geom_histogram()
```

    ## `stat_bin()` using `bins = 30`. Pick better value `binwidth`.

    ## Warning: Removed 17 rows containing non-finite outside the scale range
    ## (`stat_bin()`).

![](01_viz_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

Adding color:

``` r
weather_df |> 
  ggplot(aes(x = tmax, fill = name)) + 
  geom_histogram(position = "dodge", binwidth = 2)
```

    ## Warning: Removed 17 rows containing non-finite outside the scale range
    ## (`stat_bin()`).

![](01_viz_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

Kind of hard to understand, so make density plots instead:

``` r
weather_df |> 
  ggplot(aes(x = tmax, fill = name)) + 
  geom_density(alpha = .4, adjust = .5, color = "blue")
```

    ## Warning: Removed 17 rows containing non-finite outside the scale range
    ## (`stat_density()`).

![](01_viz_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

## Box Plots

``` r
weather_df |> 
  ggplot(aes(y = tmax)) +
  geom_boxplot()
```

    ## Warning: Removed 17 rows containing non-finite outside the scale range
    ## (`stat_boxplot()`).

![](01_viz_files/figure-gfm/unnamed-chunk-16-1.png)<!-- --> Showing
distribution of temperatures

``` r
weather_df |> 
  ggplot(aes(x = name, y = tmax)) +
  geom_boxplot()
```

    ## Warning: Removed 17 rows containing non-finite outside the scale range
    ## (`stat_boxplot()`).

![](01_viz_files/figure-gfm/unnamed-chunk-17-1.png)<!-- --> Add name
variable on x axis, do three separate plots for each of the name
variables, compare

## Violin Plots

``` r
weather_df |> 
  ggplot(aes(x = name, y = tmax)) +
  geom_violin()
```

    ## Warning: Removed 17 rows containing non-finite outside the scale range
    ## (`stat_ydensity()`).

![](01_viz_files/figure-gfm/unnamed-chunk-18-1.png)<!-- --> Same as box
plot, but now violin. Helpful for some distribution types, eg bimodal
distributions are hidden by box plots

## Ridge Plots

``` r
weather_df |> 
  ggplot(aes(x = tmax)) +
  geom_density()
```

    ## Warning: Removed 17 rows containing non-finite outside the scale range
    ## (`stat_density()`).

![](01_viz_files/figure-gfm/unnamed-chunk-19-1.png)<!-- --> This is
overall density of everything

``` r
weather_df |> 
  ggplot(aes(x = tmax, y = name)) +
  geom_density_ridges()
```

    ## Picking joint bandwidth of 1.54

    ## Warning: Removed 17 rows containing non-finite outside the scale range
    ## (`stat_density_ridges()`).

![](01_viz_files/figure-gfm/unnamed-chunk-20-1.png)<!-- --> Density
plots, but using ridges to separate out in vertical direction. Helpful
to see what is going on if you have a lot of categories (because in
density plot they all overlap)

# Save some plots

``` r
ggp_weather = 
weather_df |> 
  ggplot(aes(x = date, y = tmax, color = name)) +
  geom_point(aes(size = prcp), alpha = 0.5) +
  facet_grid(.~name)

ggp_weather
```

    ## Warning: Removed 19 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](01_viz_files/figure-gfm/unnamed-chunk-21-1.png)<!-- -->

``` r
ggsave("images/ggp_weather.pdf", ggp_weather)
```

    ## Saving 7 x 5 in image

    ## Warning: Removed 19 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

Saving plot, subdirectory/name of saved plot, which plot you’re saving
