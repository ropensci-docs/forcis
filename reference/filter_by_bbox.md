# Filter FORCIS data by a spatial bounding box

Filters FORCIS data by a spatial bounding box.

## Usage

``` r
filter_by_bbox(data, bbox)
```

## Arguments

- data:

  a `tibble` or a `data.frame`. One obtained by `read_*_data()`
  functions.

- bbox:

  an object of class `bbox` (package `sf`) or a vector of four `numeric`
  values defining a square bounding box. Values must follow this order:
  minimum longitude (`xmin`), minimum latitude (`ymin`), maximum
  longitude (`xmax`), and maximum latitude (`ymax`). **Important:** if a
  vector of numeric values is provided, coordinates must be defined in
  the system WGS 84 (`epsg=4326`).

## Value

A `tibble` containing a subset of `data` for the desired bounding box.

## Examples

``` r
# Import example dataset ----
file_name <- system.file(file.path("extdata", "FORCIS_net_sample.csv"),
                         package = "forcis")

net_data <- read.csv(file_name)

# Dimensions of the data.frame ----
dim(net_data)
#> [1] 2451   86

# Filter by oceans ----
net_data_sub <- filter_by_bbox(net_data, bbox = c(45, -61, 82, -24))

# Dimensions of the data.frame ----
dim(net_data_sub)
#> [1] 320  86
```
