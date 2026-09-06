# Map the spatial distribution of FORCIS data

Maps the spatial distribution of FORCIS data.

## Usage

``` r
ggmap_data(data, col = "red", ...)
```

## Arguments

- data:

  a `data.frame`. One obtained by `read_*_data()` functions.

- col:

  a `character` of length 1. The color of data on the map.

- ...:

  other graphical parameters passed on to
  [`geom_sf()`](https://ggplot2.tidyverse.org/reference/ggsf.html).

## Value

A `ggplot` object.

## Examples

``` r
# Import example dataset ----
file_name <- system.file(file.path("extdata", "FORCIS_net_sample.csv"),
                         package = "forcis")

net_data <- read.csv(file_name)

# Map data (default) ----
ggmap_data(net_data)


# Map data ----
ggmap_data(net_data, col = "black", fill = "red", shape = 21, size = 2)
```
