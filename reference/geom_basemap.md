# Add a World basemap to a ggplot object

Creates a World base map that can be added to a `ggplot` object. Spatial
layers come from the Natural Earth project
(<https://www.naturalearthdata.com/>) and are defined in the Robinson
coordinate system.

## Usage

``` r
geom_basemap()
```

## Value

A `ggplot` object.

## Examples

``` r
# Attach package ----
library("ggplot2")

# World basemap ----
ggplot() +
  geom_basemap()
```
