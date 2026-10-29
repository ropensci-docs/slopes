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
#> 1 bilinear     37.5ms   38.1ms      26.1   18.02MB     31.4
#> 2 simple       32.4ms   32.9ms      30.4    1.88MB     26.6
```

That is approximately

``` r

round(res$`itr/sec` * nrow(r))
#> [1] 7083 8247
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
#> 1 bilinear     38.1ms   40.9ms      24.5    1.73MB     29.4
#> 2 simple       33.6ms   34.7ms      28.5    1.81MB     24.4
```

``` r

round(res2$`itr/sec` * nrow(r))
#> [1] 6649 7722
```
