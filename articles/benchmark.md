# Benchmarking slopes calculation

``` r

library(slopes)
library(bench)
```

## Performance

A benchmark can reveal how many route gradients can be calculated per
second using different interpolation methods:

``` r

e = dem_lisbon()
r = lisbon_road_network
res = bench::mark(check = FALSE,
  bilinear = slope_raster(r, e),
  simple   = slope_raster(r, e, method = "simple")
)
```

``` r

res
#> # A tibble: 2 × 6
#>   expression      min   median `itr/sec` mem_alloc `gc/sec`
#>   <bch:expr> <bch:tm> <bch:tm>     <dbl> <bch:byt>    <dbl>
#> 1 bilinear     49.5ms   49.8ms      19.9   18.17MB     24.9
#> 2 simple       42.8ms   42.9ms      23.2    1.88MB     27.9
```

That is approximately

``` r

round(res$`itr/sec` * nrow(r))
#> [1] 5394 6298
```

routes per second using `bilinear` and `simple` interpolation methods,
respectively.

To go faster, you can chose the `simple` method to gain some speed at
the expense of accuracy:

``` r

res2 = bench::mark(check = FALSE,
  bilinear = slope_raster(r, e, method = "bilinear"),
  simple   = slope_raster(r, e, method = "simple")
)
```

``` r

res2
#> # A tibble: 2 × 6
#>   expression      min   median `itr/sec` mem_alloc `gc/sec`
#>   <bch:expr> <bch:tm> <bch:tm>     <dbl> <bch:byt>    <dbl>
#> 1 bilinear     49.7ms   53.7ms      18.6    1.73MB     23.2
#> 2 simple         44ms   44.3ms      22.4    1.81MB     18.7
```

``` r

round(res2$`itr/sec` * nrow(r))
#> [1] 5031 6080
```
