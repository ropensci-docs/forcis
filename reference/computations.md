# Compute count conversions

Functions to convert species counts between different formats: raw
abundance, relative abundance, and number concentration, using counts
metadata.

## Usage

``` r
compute_abundances(data, aggregate = TRUE)

compute_concentrations(data, aggregate = TRUE)

compute_frequencies(data, aggregate = TRUE)
```

## Arguments

- data:

  a `tibble` or a `data.frame`. One obtained by `read_*_data()`
  functions.

- aggregate:

  a `logical` of length 1. If `FALSE` counts will be derived for each
  subsample. If `TRUE` (default) subsample counts will be aggregated by
  `sample_id`.

## Value

A `tibble` in long format with two additional columns: `taxa`, the taxon
name and `counts_*`, the number concentration (`counts_n_conc`) or the
relative abundance (`counts_rel_ab`) or the raw abundance
(`counts_raw_ab`).

## Details

- `compute_concentrations()` converts all counts to number
  concentrations (n specimens/m³).

- `compute_frequencies()` converts all counts to relative abundances (%
  specimens per sampling unit).

- `compute_abundances()` converts all counts to raw abundances (n
  specimens/sampling unit).

## Examples

``` r
# Import example dataset ----
file_name <- system.file(file.path("extdata", "FORCIS_net_sample.csv"),
                         package = "forcis")

net_data <- read.csv(file_name)

# Select a taxonomy ----
net_data <- select_taxonomy(net_data, taxonomy = "VT")

# Dimensions of the data.frame ----
dim(net_data)
#> [1] 2451   80

# Compute concentration ----
net_data_conc <- compute_concentrations(net_data)
#> Counts from 14 samples could not be converted because of missing volume data
#> Relative counts from 24 samples could not be converted because of missing data on total assemblage

# Dimensions of the data.frame ----
dim(net_data_conc)
#> [1] 39032    19
```
