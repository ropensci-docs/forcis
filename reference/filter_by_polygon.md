# Filter FORCIS data by a spatial polygon

Filters FORCIS data by a spatial polygon.

## Usage

``` r
filter_by_polygon(data, polygon)
```

## Arguments

- data:

  a `tibble` or a `data.frame`. One obtained by `read_*_data()`
  functions.

- polygon:

  an `sf POLYGON` object.

## Value

A `tibble` containing a subset of `data` for the desired spatial
polygon.

## Examples

``` r
# Import example dataset ----
file_name <- system.file(file.path("extdata", "FORCIS_net_sample.csv"),
                         package = "forcis")

net_data <- read.csv(file_name)

# Dimensions of the data.frame ----
dim(net_data)
#> [1] 2451   86

# Import Indian Ocean spatial polygons ----
file_name <- system.file(file.path("extdata",
                         "IHO_Indian_ocean_polygon.gpkg"),
                         package = "forcis")

indian_ocean <- sf::st_read(file_name)
#> Reading layer `IHO_Indian_ocean_polygon' from data source 
#>   `/github/home/R/x86_64-pc-linux-gnu-library/4.6/forcis/extdata/IHO_Indian_ocean_polygon.gpkg' 
#>   using driver `GPKG'
#> Simple feature collection with 1 feature and 1 field
#> Geometry type: MULTIPOLYGON
#> Dimension:     XY
#> Bounding box:  xmin: 1508984 ymin: -6336039 xmax: 12568840 ymax: 3246966
#> Projected CRS: +proj=robin +lon_0=0 +x_0=0 +y_0=0 +datum=WGS84 +units=m +no_defs

# Filter by polygon ----
net_data_sub <- filter_by_polygon(net_data, polygon = indian_ocean)

# Dimensions of the data.frame ----
dim(net_data_sub)
#> [1] 1640   86
```
