# Data conversion

The package `forcis` provides
[functions](https://docs.ropensci.org/forcis/reference/index.html#standardization-functions)
to homogenize FORCIS data and compute abundances, concentrations, and
frequencies of foraminifera counts. This vignette shows how to use these
functions.

## Count formats

The FORCIS database includes counts of foraminifera species collected
with multiple devices. These counts are reported in different formats:

- **Raw abundance**: number of specimens counted within a sampling unit.
- **Number concentration**: number of specimens per cubic meter.
- **Relative abundance**: percentage of specimens relative to the total
  counted.
- **Fluxes**: number of specimens per square meter per day.
- **Binned counts**: number of specimens categorized into a specific
  range (minimum and maximum) within a sampling unit.

## Conversion functions

The functions detailed in this vignette allow users to convert counts
between the following formats **Raw abundance**, **Relative abundance**
and **Number concentration**.

> **NOTE:** FORCIS data from *Sediment traps* and the *CPR North* are
> not supported by these functions.

First, let’s attach the required package.

``` r

library(forcis)
```

Before proceeding, let’s download the latest version of the FORCIS
database.

``` r

# Create a data/ folder ----
dir.create("data")

# Download latest version of the database ----
download_forcis_db(path = "data", version = NULL)
```

The vignette will use the plankton net data of the FORCIS database.
Let’s import the latest release of the data.

``` r

# Import net data ----
net_data <- read_plankton_nets_data(path = "data")
```

**NB:** In this vignette, we use a subset of the plankton net data, not
the whole dataset.

After importing the data, the initial step involves choosing the
taxonomic level for the analyses, (the different taxonomic levels are
described in this [data
paper](https://www.nature.com/articles/s41597-023-02264-2)).

Let’s use the function
[`select_taxonomy()`](https://docs.ropensci.org/forcis/reference/select_taxonomy.md)
to select the **VT** taxonomy (validated taxonomy):

``` r

# Select taxonomy ----
net_data_vt <- net_data |>
  select_taxonomy(taxonomy = "VT")
```

Once the data contain counts from the same taxonomic level, we can
proceed with the conversion functions: `compute_*()`.

The functions accept two arguments: the input `data` and the `aggregate`
arguments. If `aggregate = TRUE`, the function will return the
transformed counts of each species using the sample as the unit. If
`aggregate = FALSE`, it will re-calculate the species’ abundance by
subsample.

### `compute_abundances()`

This function converts all counts into raw abundances, using sampling
metadata such as sample volume and total assemblage counts. It
calculates the raw abundance for each taxon whose counts are reported as
either relative abundance or number concentrations.

``` r

# Convert species counts in raw abundance ----
net_data_vt_raw_ab <- net_data_vt |>
  compute_abundances(aggregate = TRUE)
#> Counts from 26 samples could not be converted because of missing volume data
#> Relative counts from 24 samples could not be converted because of missing data on total assemblage
```

``` r

# Format ----
dim(net_data_vt)
#> [1] 2451   80
dim(net_data_vt_raw_ab)
#> [1] 39032    19

# Header ----
net_data_vt_raw_ab |>
  as.data.frame() |>
  head()
#>   data_type cruise_id profile_id sample_id sample_min_depth sample_max_depth
#> 1       Net     MD193      A3_C1 A3_C1_S10               80              100
#> 2       Net     MD193      A3_C1 A3_C1_S10               80              100
#> 3       Net     MD193      A3_C1 A3_C1_S10               80              100
#> 4       Net     MD193      A3_C1 A3_C1_S10               80              100
#> 5       Net     MD193      A3_C1 A3_C1_S10               80              100
#> 6       Net     MD193      A3_C1 A3_C1_S10               80              100
#>   profile_depth_min profile_depth_max profile_date_time cast_net_op_m2
#> 1                 0               100        21/02/2013           0.25
#> 2                 0               100        21/02/2013           0.25
#> 3                 0               100        21/02/2013           0.25
#> 4                 0               100        21/02/2013           0.25
#> 5                 0               100        21/02/2013           0.25
#> 6                 0               100        21/02/2013           0.25
#>   sample_segment_length site_lat_start_decimal site_lon_start_decimal
#> 1                    NA                 -50.37                     72
#> 2                    NA                 -50.37                     72
#> 3                    NA                 -50.37                     72
#> 4                    NA                 -50.37                     72
#> 5                    NA                 -50.37                     72
#> 6                    NA                 -50.37                     72
#>   sample_volume_filtered site_id cast_id sample_sst                        taxa
#> 1                      5      A3   A3_C1       3.09               b_digitata_VT
#> 2                      5      A3   A3_C1       3.09 g_truncatulinoides_right_VT
#> 3                      5      A3   A3_C1       3.09                  g_uvula_VT
#> 4                      5      A3   A3_C1       3.09                g_inflata_VT
#> 5                      5      A3   A3_C1       3.09               g_tenellus_VT
#> 6                      5      A3   A3_C1       3.09              n_dutertrei_VT
#>   counts_raw_ab
#> 1             0
#> 2             0
#> 3            63
#> 4             0
#> 5             0
#> 6             1
```

The functions `compute_*()` output a table in a long-format as well as a
message reporting the amount of data that could not be converted because
of missing metadata.

### `compute_concentrations()`

This function transforms all counts into number concentration
abundances. It also leverages sampling metadata such as sample volume
and total assemblage counts to compute the number concentration for each
species.

``` r

# Convert species counts in number concentration ----
net_data_vt_n_conc <- net_data_vt |>
  compute_concentrations(aggregate = TRUE)
#> Counts from 14 samples could not be converted because of missing volume data
#> Relative counts from 24 samples could not be converted because of missing data on total assemblage
```

### `compute_frequencies()`

This function computes relative abundance for each species using total
assemblage counts when available.

``` r

# Convert species counts in relative abundance ----
net_data_rel_ab <- net_data_vt |>
  compute_frequencies(aggregate = TRUE)
#> Counts from 14 samples could not be converted because of missing volume data
#> Counts from 0 samples could not be converted because of missing data on total assemblage
```
