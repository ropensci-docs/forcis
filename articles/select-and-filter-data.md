# Select, reshape, and filter data

The package `forcis` provides [a lot of
functions](https://docs.ropensci.org/forcis/reference/index.html#select-and-filters-tools)
to filter, reshape, and select FORCIS data. This vignette shows how to
use these functions. With the exception of
[`select_taxonomy()`](https://docs.ropensci.org/forcis/reference/select_taxonomy.md),
all functions presented in this vignette are optional and depend on your
research questions. You can filter data by species, time range, ocean,
etc.

## Setup

First, let’s import the required packages.

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

The vignette will use the plankton nets data of the FORCIS database.
Let’s import the latest release of the data.

``` r

# Import net data ----
net_data <- read_plankton_nets_data(path = "data")
```

**NB:** In this vignette, we use a subset of the plankton nets data, not
the whole dataset.

## Selecting columns

### Select a taxonomy

The FORCIS database provides three different taxonomies:

- `OT`: original taxonomy, i.e. the initial list of species names and
  attributes (e.g., shell pigmentation, coiling direction) as reported
  in various datasets and studies.
- `VT`: validated taxonomy, i.e. a refined version of the original
  taxonomy that resolves issues of synonymy (different names for the
  same taxon) and shifting taxonomic concepts.
- `LT`: lumped taxonomy, i.e. a simplified version of the validated
  taxonomy. It merges taxa that are difficult to distinguish across
  datasets (morphospecies), ensuring consistency and comparability in
  broader analyses.

See the [associated data
paper](https://doi.org/10.1038/s41597-023-02264-2) for further
information.

After importing the data and before going any further, the next step
involves choosing the taxonomic level for the analyses. **This is
mandatory to avoid duplicated records**.

Let’s use the function
[`select_taxonomy()`](https://docs.ropensci.org/forcis/reference/select_taxonomy.md)
to select the **VT** taxonomy (validated taxonomy):

``` r

# Select taxonomy ----
net_data_vt <- net_data |>
  select_taxonomy(taxonomy = "VT")

net_data_vt
#> # A tibble: 2,451 × 80
#>    data_type cruise_id    profile_id sample_id sample_min_depth sample_max_depth
#>    <chr>     <chr>        <chr>      <chr>                <dbl>            <dbl>
#>  1 Net       ATLANTIS_II… ATLANTIS_… ATLANTIS…                0               86
#>  2 Net       ATLANTIS_II… ATLANTIS_… ATLANTIS…                0               86
#>  3 Net       ATLANTIS_II… ATLANTIS_… ATLANTIS…                0              118
#>  4 Net       ATLANTIS_II… ATLANTIS_… ATLANTIS…                0              106
#>  5 Net       ATLANTIS_II… ATLANTIS_… ATLANTIS…                0              118
#>  6 Net       ATLANTIS_II… ATLANTIS_… ATLANTIS…                0               86
#>  7 Net       ATLANTIS_II… ATLANTIS_… ATLANTIS…                0               64
#>  8 Net       ATLANTIS_II… ATLANTIS_… ATLANTIS…                0               73
#>  9 Net       ATLANTIS_II… ATLANTIS_… ATLANTIS…                0               83
#> 10 Net       ATLANTIS_II… ATLANTIS_… ATLANTIS…                0              127
#> # ℹ 2,441 more rows
#> # ℹ 74 more variables: profile_depth_min <int>, profile_depth_max <dbl>,
#> #   profile_date_time <chr>, cast_net_op_m2 <dbl>, subsample_id <chr>,
#> #   sample_segment_length <lgl>, subsample_count_type <chr>,
#> #   subsample_size_fraction_min <int>, subsample_size_fraction_max <int>,
#> #   site_lat_start_decimal <dbl>, site_lon_start_decimal <dbl>,
#> #   sample_volume_filtered <dbl>, …
```

### Select required columns

Because FORCIS data contain more than 100 columns, the function
[`select_forcis_columns()`](https://docs.ropensci.org/forcis/reference/select_forcis_columns.md)
can be used to lighten the data to easily handle it and to speed up some
computations.

By default, only required columns listed in
[`get_required_columns()`](https://docs.ropensci.org/forcis/reference/get_required_columns.md)
(required by some functions of the package like `compute_*()` and
`plot_*()`) and species columns will be kept.

``` r

# Remove not required columns (optional) ----
net_data_vt <- net_data_vt |>
  select_forcis_columns()

net_data_vt
#> # A tibble: 2,451 × 77
#>    data_type cruise_id    profile_id sample_id sample_min_depth sample_max_depth
#>    <chr>     <chr>        <chr>      <chr>                <dbl>            <dbl>
#>  1 Net       ATLANTIS_II… ATLANTIS_… ATLANTIS…                0               86
#>  2 Net       ATLANTIS_II… ATLANTIS_… ATLANTIS…                0               86
#>  3 Net       ATLANTIS_II… ATLANTIS_… ATLANTIS…                0              118
#>  4 Net       ATLANTIS_II… ATLANTIS_… ATLANTIS…                0              106
#>  5 Net       ATLANTIS_II… ATLANTIS_… ATLANTIS…                0              118
#>  6 Net       ATLANTIS_II… ATLANTIS_… ATLANTIS…                0               86
#>  7 Net       ATLANTIS_II… ATLANTIS_… ATLANTIS…                0               64
#>  8 Net       ATLANTIS_II… ATLANTIS_… ATLANTIS…                0               73
#>  9 Net       ATLANTIS_II… ATLANTIS_… ATLANTIS…                0               83
#> 10 Net       ATLANTIS_II… ATLANTIS_… ATLANTIS…                0              127
#> # ℹ 2,441 more rows
#> # ℹ 71 more variables: profile_depth_min <int>, profile_depth_max <dbl>,
#> #   profile_date_time <chr>, cast_net_op_m2 <dbl>, subsample_id <chr>,
#> #   sample_segment_length <lgl>, subsample_count_type <chr>,
#> #   subsample_size_fraction_min <int>, subsample_size_fraction_max <int>,
#> #   site_lat_start_decimal <dbl>, site_lon_start_decimal <dbl>,
#> #   sample_volume_filtered <dbl>, …
```

You can also use the argument `cols` to keep additional columns.

## Filtering rows

The `filter_by_*()` functions are optional and their use depends on your
research questions.

### Filter by month of data collection

The
[`filter_by_month()`](https://docs.ropensci.org/forcis/reference/filter_by_month.md)
function filters observations based on the **month of sampling**. It
requires two arguments: the data and a numeric vector with values
between 1 and 12.

``` r

# Filter data by sampling month ----
net_data_vt_july_aug <- net_data_vt |>
  filter_by_month(months = 7:8)

# Number of original records ----
nrow(net_data_vt)
#> [1] 2451

# Number of filtered records ----
nrow(net_data_vt_july_aug)
#> [1] 516
```

### Filter by year of data collection

The
[`filter_by_year()`](https://docs.ropensci.org/forcis/reference/filter_by_year.md)
function filters observations based on the **year of sampling**. It
requires two arguments: the data and a numeric vector with the years of
interest.

``` r

# Filter data by sampling year ----
net_data_vt_9020 <- net_data_vt |>
  filter_by_year(years = 1990:2020)

# Number of original records ----
nrow(net_data_vt)
#> [1] 2451

# Number of filtered records ----
nrow(net_data_vt_9020)
#> [1] 2283
```

### Filter by bounding box

The function
[`filter_by_bbox()`](https://docs.ropensci.org/forcis/reference/filter_by_bbox.md)
can be used to filter FORCIS data by a spatial bounding box (argument
`bbox`).

Let’s filter the plankton net data by a spatial rectangle located in the
Indian ocean.

``` r

# Filter by spatial bounding box ----
net_data_vt_bbox <- net_data_vt |>
  filter_by_bbox(bbox = c(45, -61, 82, -24))

# Number of original records ----
nrow(net_data_vt)
#> [1] 2451

# Number of filtered records ----
nrow(net_data_vt_bbox)
#> [1] 320
```

Note that the argument `bbox` can be either an object of class `bbox`
(package `sf`) or a vector of four numeric values defining a square
bounding box. If a vector of numeric values is provided, coordinates
must be defined in the system WGS 84 (`epsg=4326`).

Let’s check the spatial extent by converting these two `tibbles` into
spatial layers (`sf` objects) with the function
[`data_to_sf()`](https://docs.ropensci.org/forcis/reference/data_to_sf.md).

``` r

# Filter by spatial bounding box ----
net_data_vt_sf <- net_data_vt |>
  data_to_sf()

net_data_vt_bbox_sf <- net_data_vt_bbox |>
  data_to_sf()

# Original spatial extent ----
sf::st_bbox(net_data_vt_sf)
#>       xmin       ymin       xmax       ymax 
#>  -809816.4 -5989270.6 11259385.1  8116790.4

# Spatial extent of filtered records ----
sf::st_bbox(net_data_vt_bbox_sf)
#>     xmin     ymin     xmax     ymax 
#>  4407928 -5989271  6704380 -3208558
```

### Filter by ocean

The function
[`filter_by_ocean()`](https://docs.ropensci.org/forcis/reference/filter_by_ocean.md)
can be used to filter FORCIS data by one or several oceans (argument
`ocean`).

Let’s filter the plankton net data located in the Indian ocean.

``` r

# Filter by ocean name ----
net_data_vt_indian <- net_data_vt |>
  filter_by_ocean(ocean = "Indian Ocean")

# Number of original records ----
nrow(net_data_vt)
#> [1] 2451

# Number of filtered records ----
nrow(net_data_vt_indian)
#> [1] 1640
```

Use the function
[`get_ocean_names()`](https://docs.ropensci.org/forcis/reference/get_ocean_names.md)
to retrieve the name of World oceans according to the IHO Sea Areas
dataset version 3 (used in this package).

``` r

# Get ocean names ----
get_ocean_names()
#> [1] "Arctic Ocean"         "Indian Ocean"         "Mediterranean Sea"   
#> [4] "North Atlantic Ocean" "North Pacific Ocean"  "South Atlantic Ocean"
#> [7] "South Pacific Ocean"  "Southern Ocean"
```

### Filter by spatial polygon

The function
[`filter_by_polygon()`](https://docs.ropensci.org/forcis/reference/filter_by_polygon.md)
can be used to filter FORCIS data a spatial polygon (argument
`polygon`).

Let’s filter the plankton net data by a spatial polygon defining
boundaries of the Indian ocean.

``` r

# Import spatial polygon ----
file_name <- system.file(
  file.path("extdata", "IHO_Indian_ocean_polygon.gpkg"),
  package = "forcis"
)

indian_ocean <- sf::st_read(file_name, quiet = TRUE)

# Filter by polygon ----
net_data_vt_poly <- net_data_vt |>
  filter_by_polygon(polygon = indian_ocean)

# Number of original records ----
nrow(net_data_vt)
#> [1] 2451

# Number of filtered records ----
nrow(net_data_vt_poly)
#> [1] 1640
```

### Filter by species

The
[`filter_by_species()`](https://docs.ropensci.org/forcis/reference/filter_by_species.md)
function allows users to filter FORCIS data for one or more species.

It takes a `data.frame` (or a `tibble`) and a vector of species names
(argument `species`).

Let’s subset plankton net data to only keep only two species: *G.
glutinata* and *C. nitida*.

``` r

# Filter by species ----
net_data_vt_glutinata_nitida <- net_data_vt |>
  filter_by_species(species = c("g_glutinata_VT", "c_nitida_VT"))

# Dimensions of original data ----
dim(net_data_vt)
#> [1] 2451   77

# Dimensions of filtered data ----
dim(net_data_vt_glutinata_nitida)
#> [1] 2451   23
```

**Important:** The
[`filter_by_species()`](https://docs.ropensci.org/forcis/reference/filter_by_species.md)
function does not remove rows (samples) but columns: it removes other
species columns. To only keep samples where these two species have been
detected, we can use:

``` r

# Keep samples with positive counts ----
net_data_vt_glutinata_nitida <- net_data_vt_glutinata_nitida |>
  dplyr::filter(g_glutinata_VT > 0 | c_nitida_VT > 0)

# Number of filtered records ----
nrow(net_data_vt_glutinata_nitida)
#> [1] 1013
```

## Reshaping

### Convert to long format

The
[`convert_to_long_format()`](https://docs.ropensci.org/forcis/reference/convert_to_long_format.md)
function converts FORCIS data into a long format.

``` r

# Convert to long format ----
net_data_long <- convert_to_long_format(net_data)

# Dimensions of original data ----
dim(net_data)
#> [1] 2451   86

# Dimensions of reshaped data ----
dim(net_data_long)
#> [1] 151962     23
```

Two columns have been created: `taxa` (taxon names) and `counts` (taxon
counts).

``` r

# Column names ----
colnames(net_data_long)
#>  [1] "data_type"                                
#>  [2] "cruise_id"                                
#>  [3] "profile_id"                               
#>  [4] "sample_id"                                
#>  [5] "sample_min_depth"                         
#>  [6] "sample_max_depth"                         
#>  [7] "profile_depth_min"                        
#>  [8] "profile_depth_max"                        
#>  [9] "profile_date_time"                        
#> [10] "cast_net_op_m2"                           
#> [11] "subsample_id"                             
#> [12] "sample_segment_length"                    
#> [13] "subsample_count_type"                     
#> [14] "subsample_size_fraction_min"              
#> [15] "subsample_size_fraction_max"              
#> [16] "site_lat_start_decimal"                   
#> [17] "site_lon_start_decimal"                   
#> [18] "sample_volume_filtered"                   
#> [19] "subsample_all_shells_present_were_counted"
#> [20] "total_of_forams_counted_ind"              
#> [21] "sampling_device_type"                     
#> [22] "taxa"                                     
#> [23] "counts"
```
