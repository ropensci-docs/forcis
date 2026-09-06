# Convert a data frame into an sf object

This function can be used to convert a `data.frame` into an `sf` object.
Note that coordinates (columns `site_lon_start_decimal` and
`site_lat_start_decimal`) are projected in the Robinson coordinate
system.

## Usage

``` r
data_to_sf(data)
```

## Arguments

- data:

  a `tibble` or a `data.frame`, i.e. a FORCIS dataset or the output of a
  `filter_*()` function.

## Value

An `sf POINTS` object.

## Examples

``` r
# Attach package ----
library("ggplot2")

# Import example dataset ----
file_name <- system.file(file.path("extdata", "FORCIS_net_sample.csv"),
                         package = "forcis")

net_data <- read.csv(file_name)

# Dimensions of the data.frame ----
dim(net_data)
#> [1] 2451   86

# Filter by years ----
net_data_sub <- filter_by_year(net_data, years = 1992)

# Convert to an sf object ----
net_data_sub_sf <- data_to_sf(net_data_sub)

# World basemap ----
ggplot() +
  geom_basemap() +
  geom_sf(data = net_data_sub_sf)
```
