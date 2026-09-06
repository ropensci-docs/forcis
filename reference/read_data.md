# Read FORCIS data

These functions read one specific `csv` file of the FORCIS database (see
below) stored in the folder `path`. The function
[`download_forcis_db()`](https://docs.ropensci.org/forcis/reference/download_forcis_db.md)
must be used first to store locally the database.

## Usage

``` r
read_cpr_north_data(
  path,
  version = options()$forcis_version,
  check_for_update = options()$forcis_check_for_update
)

read_cpr_south_data(
  path,
  version = options()$forcis_version,
  check_for_update = options()$forcis_check_for_update
)

read_plankton_nets_data(
  path,
  version = options()$forcis_version,
  check_for_update = options()$forcis_check_for_update
)

read_pump_data(
  path,
  version = options()$forcis_version,
  check_for_update = options()$forcis_check_for_update
)

read_sediment_trap_data(
  path,
  version = options()$forcis_version,
  check_for_update = options()$forcis_check_for_update
)
```

## Arguments

- path:

  a `character` of length 1. The folder in which the FORCIS database has
  been saved.

- version:

  a `character` of length 1. The version number (with two numbers, e.g.
  `08` instead of `8`) of the FORCIS database to use. Default is the
  latest version. Note that this argument can be handle with the global
  option `forcis_version`. For example, if user calls
  `options(forcis_version = "07")`, the version `07` will be used by
  default for the current R session. Note that it is recommended to use
  the latest version of the database.

- check_for_update:

  a `logical`. If `TRUE` (default) the function will check if a newer
  version of the FORCIS database is available on Zenodo and will print
  an informative message. Note that this argument can be handle with the
  global option `forcis_check_for_update`. For example, if user calls
  `options(forcis_check_for_update = FALSE)`, the message to download
  the latest version will be disabled for the current R session.

## Value

A `tibble`. See <https://zenodo.org/doi/10.5281/zenodo.7390791> for a
preview of the datasets.

## Details

- `read_plankton_nets_data()` reads the FORCIS plankton nets data

- `read_pump_data()` reads the FORCIS pump data

- `read_cpr_north_data()` reads the FORCIS CPR North data

- `read_cpr_south_data()` reads the FORCIS CPR South data

- `read_sediment_trap_data()` reads the FORCIS sediment traps data

## See also

[`download_forcis_db()`](https://docs.ropensci.org/forcis/reference/download_forcis_db.md)
to download the complete FORCIS database.

## Examples

``` r
# \donttest{
# Folder in which the database will be saved ----
# N.B. In this example we use a temporary folder but you should select an
# existing folder (for instance "data/").
path <- tempdir()

# Download the database ----
download_forcis_db(path, timeout = 300)
#> The file 'iho_oceans_boundaries.rds' already exists. If you want to download again this file please use the argument 'overwrite'.
#> The file 'FORCIS_cpr_north_11072024.csv' already exists. If you want to download again this file please use the argument 'overwrite'.
#> The file 'FORCIS_data_template.xlsx' already exists. If you want to download again this file please use the argument 'overwrite'.
#> The file 'FORCIS_taxonomy_levels.xlsx' already exists. If you want to download again this file please use the argument 'overwrite'.
#> The file 'FORCIS_net_11072024.csv' already exists. If you want to download again this file please use the argument 'overwrite'.
#> The file 'FORCIS_cpr_south_11072024.csv' already exists. If you want to download again this file please use the argument 'overwrite'.
#> The file 'FORCIS_pump_11072024.csv' already exists. If you want to download again this file please use the argument 'overwrite'.
#> The file 'FORCIS_trap_11072024.csv' already exists. If you want to download again this file please use the argument 'overwrite'.

# Import plankton nets data ----
plankton_nets_data <- read_plankton_nets_data(path)
# }
```
