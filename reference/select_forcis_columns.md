# Select columns in FORCIS data

Selects columns in FORCIS data. Because FORCIS data contains more than
100 columns, this function can be used to lighten the `data.frame` to
easily handle it and to speed up some computations.

## Usage

``` r
select_forcis_columns(data, cols = NULL)
```

## Arguments

- data:

  a `tibble` or a `data.frame`. One obtained by `read_*_data()`
  functions.

- cols:

  a `character` vector of column names to keep in addition to the
  required ones (see
  [`get_required_columns()`](https://docs.ropensci.org/forcis/reference/get_required_columns.md))
  and to the taxa columns. Can be `NULL` (default).

## Value

A `tibble`.

## Examples

``` r
# Import example dataset ----
file_name <- system.file(file.path("extdata", "FORCIS_net_sample.csv"),
                         package = "forcis")

net_data <- read.csv(file_name)

# Dimensions of the data.frame ----
dim(net_data)
#> [1] 2451   86

# Select a taxonomy ----
net_data <- select_taxonomy(net_data, taxonomy = "VT")

# Dimensions of the data.frame ----
dim(net_data)
#> [1] 2451   80

# Select only required columns (and taxa) ----
net_data <- select_forcis_columns(net_data)

# Dimensions of the data.frame ----
dim(net_data)
#> [1] 2451   77
```
