# Download the FORCIS database

Downloads the entire FORCIS database as a collection of five `csv` files
from Zenodo (<https://zenodo.org/doi/10.5281/zenodo.7390791>).
Additional files will be also downloaded.

## Usage

``` r
download_forcis_db(
  path,
  version = options()$forcis_version,
  check_for_update = options()$forcis_check_for_update,
  overwrite = FALSE,
  timeout = 60
)
```

## Arguments

- path:

  a `character` of length 1. The folder in which the FORCIS database
  will be saved. Note that a subdirectory will be created, e.g.
  `forcis-db/version-99/` (with `99` the version number).

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

- overwrite:

  a `logical`. If `TRUE` it will override the downloaded files of the
  FORCIS database. Default is `FALSE`.

- timeout:

  an `integer`. The timeout for downloading files from Zenodo. Default
  is `60`. This number can be increased for low Internet connection.

## Value

No return value. The FORCIS files will be saved in the `path` folder.

## Details

The FORCIS database is regularly updated. The global structure of the
tables doesn’t change between versions but some bugs can be fixed and
new records can be added. This is why it is recommended to use the
latest version of the database. The package is designed to handle the
versioning of the database on Zenodo and will inform the user if a new
version is available each time he/she uses one of the `read_*_data()`
functions.

For more information, please read the vignette available at
<https://docs.ropensci.org/forcis/articles/database-versions.html>.

## References

Chaabane S, De Garidel-Thoron T, Giraud X, *et al.* (2023) The FORCIS
database: A global census of planktonic Foraminifera from ocean waters.
*Scientific Data*, 10, 354. DOI:
[doi:10.1038/s41597-023-02264-2](https://doi.org/10.1038/s41597-023-02264-2)
.

## See also

[`read_plankton_nets_data()`](https://docs.ropensci.org/forcis/reference/read_data.md)
to import the FORCIS database.

## Examples

``` r
# \donttest{
# Folder in which the database will be saved ----
# N.B. In this example we use a temporary folder but you should select an
# existing folder (for instance "data/").
path <- tempdir()

# Download the database ----
download_forcis_db(path, timeout = 300)
#> The file 'iho_oceans_boundaries.rds' has been successfully downloaded
#> The file 'FORCIS_cpr_north_11072024.csv' has been successfully downloaded
#> The file 'FORCIS_data_template.xlsx' has been successfully downloaded
#> The file 'FORCIS_taxonomy_levels.xlsx' has been successfully downloaded
#> The file 'FORCIS_net_11072024.csv' has been successfully downloaded
#> The file 'FORCIS_cpr_south_11072024.csv' has been successfully downloaded
#> The file 'FORCIS_pump_11072024.csv' has been successfully downloaded
#> The file 'FORCIS_trap_11072024.csv' has been successfully downloaded

# Check the content of the folder ----
list.files(path, recursive = TRUE)
#>  [1] "bslib-e48b6721a0c9defbd834a66ffec6e510/bootstrap.bundle.min.js"    
#>  [2] "bslib-e48b6721a0c9defbd834a66ffec6e510/bootstrap.bundle.min.js.map"
#>  [3] "bslib-e48b6721a0c9defbd834a66ffec6e510/bootstrap.min.css"          
#>  [4] "downlit/base"                                                      
#>  [5] "downlit/ggplot2"                                                   
#>  [6] "downlit/remotes"                                                   
#>  [7] "downlit/rmarkdown"                                                 
#>  [8] "downlit/utils"                                                     
#>  [9] "file616394bb92"                                                    
#> [10] "file6166a5a3012"                                                   
#> [11] "file616716afe1"                                                    
#> [12] "forcis-db/version-10/FORCIS_cpr_north_11072024.csv"                
#> [13] "forcis-db/version-10/FORCIS_cpr_south_11072024.csv"                
#> [14] "forcis-db/version-10/FORCIS_data_template.xlsx"                    
#> [15] "forcis-db/version-10/FORCIS_net_11072024.csv"                      
#> [16] "forcis-db/version-10/FORCIS_pump_11072024.csv"                     
#> [17] "forcis-db/version-10/FORCIS_taxonomy_levels.xlsx"                  
#> [18] "forcis-db/version-10/FORCIS_trap_11072024.csv"                     
#> [19] "forcis-db/version-10/iho_oceans_boundaries.rds"                    
# }
```
