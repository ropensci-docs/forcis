# Filter FORCIS data by month of sampling

Filters FORCIS data by month of sampling.

## Usage

``` r
filter_by_month(data, months)
```

## Arguments

- data:

  a `tibble` or a `data.frame`. One obtained by `read_*_data()`
  functions.

- months:

  a `numeric` containing one or several months.

## Value

A `tibble` containing a subset of `data` for the desired months.

## Examples

``` r
# Import example dataset ----
file_name <- system.file(file.path("extdata", "FORCIS_net_sample.csv"),
                         package = "forcis")

net_data <- read.csv(file_name)

# Dimensions of the data.frame ----
dim(net_data)
#> [1] 2451   86

# Filter by months ----
net_data_sub <- filter_by_month(net_data, months = 1:2)

# Dimensions of the data.frame ----
dim(net_data_sub)
#> [1] 305  86
```
