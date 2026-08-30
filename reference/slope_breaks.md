# Recommended slope break thresholds (as proportions)

A numeric vector of seven break points in **proportion units** (e.g.
0.05 = 5\\ Defines six slope severity classes for use with
[`slope_colors`](https://docs.ropensci.org/slopes/reference/slope_colors.md):
0–3\\

## Usage

``` r
slope_breaks
```

## Format

A numeric vector of length 7.

## Details

Use with `cut(slope_values, breaks = slope_breaks)` where slope values
are proportions as returned by
[`slope_xyz`](https://docs.ropensci.org/slopes/reference/slope_xyz.md).

## See also

[`slope_colors`](https://docs.ropensci.org/slopes/reference/slope_colors.md),
[`plot_slope`](https://docs.ropensci.org/slopes/reference/plot_slope.md)

## Examples

``` r
slope_breaks
#> [1] 0.00 0.03 0.05 0.08 0.10 0.20  Inf
```
