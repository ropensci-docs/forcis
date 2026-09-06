# Filter FORCIS data by year of sampling

Filters FORCIS data by year of sampling.

## Usage

``` r
filter_by_year(data, years)
```

## Arguments

- data:

  a `tibble` or a `data.frame`. One obtained by `read_*_data()`
  functions.

- years:

  a `numeric` containing one or several years.

## Value

A `tibble` containing a subset of `data` for the desired years.

## Examples

``` r
# Import example dataset ----
file_name <- system.file(file.path("extdata", "FORCIS_net_sample.csv"),
                         package = "forcis")

net_data <- read.csv(file_name)

# Dimensions of the data.frame ----
dim(net_data)
#> [1] 2451   86

# Filter by years ----
net_data_sub <- filter_by_year(net_data, years = 1992)

# Dimensions of the data.frame ----
dim(net_data_sub)
#> [1] 610  86
```
