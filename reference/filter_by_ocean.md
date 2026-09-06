# Filter FORCIS data by ocean

Filters FORCIS data by one or several oceans.

## Usage

``` r
filter_by_ocean(data, ocean)
```

## Arguments

- data:

  a `tibble` or a `data.frame`. One obtained by `read_*_data()`
  functions.

- ocean:

  a `character` vector of one or several ocean names. Use the function
  [`get_ocean_names()`](https://docs.ropensci.org/forcis/reference/get_ocean_names.md)
  to find the correct spelling.

## Value

A `tibble` containing a subset of `data` for the desired oceans.

## Examples

``` r
# Import example dataset ----
file_name <- system.file(file.path("extdata", "FORCIS_net_sample.csv"),
                         package = "forcis")

net_data <- read.csv(file_name)

# Dimensions of the data.frame ----
dim(net_data)
#> [1] 2451   86

# Get ocean names ----
get_ocean_names()
#> [1] "Arctic Ocean"         "Indian Ocean"         "Mediterranean Sea"   
#> [4] "North Atlantic Ocean" "North Pacific Ocean"  "South Atlantic Ocean"
#> [7] "South Pacific Ocean"  "Southern Ocean"      

# Filter by oceans ----
net_data_sub <- filter_by_ocean(net_data, ocean = "Indian Ocean")

# Dimensions of the data.frame ----
dim(net_data_sub)
#> [1] 1640   86
```
