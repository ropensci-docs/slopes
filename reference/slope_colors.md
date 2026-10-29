# Recommended slope colours (dark green to dark red)

A character vector of six hex colours ranging from dark green (flat,
\\\le\\3\\ to dark red (steep, \>20\\ Use directly with
[`slope_breaks`](https://docs.ropensci.org/slopes/reference/slope_breaks.md)
and [`cut()`](https://rdrr.io/r/base/cut.html) to colour segments by
slope proportion (as returned by
[`slope_xyz`](https://docs.ropensci.org/slopes/reference/slope_xyz.md)).

## Usage

``` r
slope_colors
```

## Format

A character vector of length 6.

## See also

[`slope_breaks`](https://docs.ropensci.org/slopes/reference/slope_breaks.md),
[`plot_slope`](https://docs.ropensci.org/slopes/reference/plot_slope.md)

## Examples

``` r
slope_colors
#> [1] "#267300" "#70A800" "#FFAA00" "#E60000" "#A80000" "#730000"
# \donttest{
route_xyz <- elevation_add(lisbon_route, dem = dem_lisbon())

# 1. Colour segments by steepness (ignoring direction) using abs()
segs <- route_to_segments(route_xyz)
segs$slope <- slope_xyz(segs)
col_idx <- cut(abs(segs$slope), breaks = slope_breaks,
  labels = FALSE, include.lowest = TRUE)
plot(sf::st_geometry(segs), col = slope_colors[col_idx], lwd = 3)


# 2. Symmetric palette for plot_slope(): green = gentle, red = steep either way
plot_slope(route_xyz, pal = c(rev(slope_colors), slope_colors))

# }
```
