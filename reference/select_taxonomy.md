# Select a taxonomy in FORCIS data

Selects a taxonomy in FORCIS data. FORCIS database provides three
different taxonomies: `"LT"` (lumped taxonomy), `"VT"` (validated
taxonomy) and `"OT"` (original taxonomy). See
[doi:10.1038/s41597-023-02264-2](https://doi.org/10.1038/s41597-023-02264-2)
for further information.

## Usage

``` r
select_taxonomy(data, taxonomy)
```

## Arguments

- data:

  a `tibble` or a `data.frame`. One obtained by `read_*_data()`
  functions.

- taxonomy:

  a `character` of length 1. One among `"LT"`, `"VT"`, `"OT"`.

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
```
