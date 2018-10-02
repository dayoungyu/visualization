### Visualization Pt 2

    library(rnoaa)

    weather_df = 
      rnoaa::meteo_pull_monitors(c("USW00094728", "USC00519397", "USS0023B17S"),
                          var = c("PRCP", "TMIN", "TMAX"), 
                          date_min = "2017-01-01",
                          date_max = "2017-12-31") %>%
      mutate(
        name = recode(id, USW00094728 = "CentralPark_NY", 
                          USC00519397 = "Waikiki_HA",
                          USS0023B17S = "Waterhole_WA"),
        tmin = tmin / 10,
        tmax = tmax / 10) %>%
      select(name, id, everything())
    weather_df

    ## # A tibble: 1,095 x 6
    ##    name           id          date        prcp  tmax  tmin
    ##    <chr>          <chr>       <date>     <dbl> <dbl> <dbl>
    ##  1 CentralPark_NY USW00094728 2017-01-01     0   8.9   4.4
    ##  2 CentralPark_NY USW00094728 2017-01-02    53   5     2.8
    ##  3 CentralPark_NY USW00094728 2017-01-03   147   6.1   3.9
    ##  4 CentralPark_NY USW00094728 2017-01-04     0  11.1   1.1
    ##  5 CentralPark_NY USW00094728 2017-01-05     0   1.1  -2.7
    ##  6 CentralPark_NY USW00094728 2017-01-06    13   0.6  -3.8
    ##  7 CentralPark_NY USW00094728 2017-01-07    81  -3.2  -6.6
    ##  8 CentralPark_NY USW00094728 2017-01-08     0  -3.8  -8.8
    ##  9 CentralPark_NY USW00094728 2017-01-09     0  -4.9  -9.9
    ## 10 CentralPark_NY USW00094728 2017-01-10     0   7.8  -6  
    ## # ... with 1,085 more rows

Start a plot
------------

First scatterplot

    ggplot(weather_df, aes(x = tmin, y = tmax)) + 
      geom_point(aes(color = name), alpha = .5) +
      labs(
        title = "Temperature plot",
        x = "Minimum daily temperature (C)",
        y = "Maxiumum daily temperature (C)",
        caption = "Data from the rnoaa package"
      )

    ## Warning: Removed 15 rows containing missing values (geom_point).

<img src="vix_ii_files/figure-markdown_strict/unnamed-chunk-2-1.png" width="90%" />

Tick marks and labels...

    ggplot(weather_df, aes(x = tmin, y = tmax)) + 
      geom_point(aes(color = name), alpha = .5) +
      labs(
        title = "Temperature plot",
        x = "Minimum daily temperature (C)",
        y = "Maxiumum daily temperature (C)",
        caption = "Data from the rnoaa package"
      ) +
      scale_x_continuous(
        breaks = c(-15, 0, 15),
        labels = c("-15º C", "0º C", "15"),
        limits = c(-20, 32)
      ) +
      scale_y_continuous(
        trans = "sqrt", 
        position = "right")

    ## Warning in self$trans$transform(x): NaNs produced

    ## Warning: Transformation introduced infinite values in continuous y-axis

    ## Warning: Removed 90 rows containing missing values (geom_point).

<img src="vix_ii_files/figure-markdown_strict/unnamed-chunk-3-1.png" width="90%" />

Colors and themes
-----------------
