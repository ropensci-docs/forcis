# Get available versions of the FORCIS database

Gets all available versions of the FORCIS database by querying the
Zenodo API (<https://developers.zenodo.org>).

## Usage

``` r
get_available_versions()
```

## Value

A `tibble` with three columns:

- `publication_date`: the date of the release of the version

- `version`: the label of the version

- `access_right`: is the version open or restricted?

## Examples

``` r
# \donttest{
# Versions of the FORCIS database ----
get_available_versions()
#> # A tibble: 10 × 3
#>    publication_date version access_right
#>    <chr>            <chr>   <chr>       
#>  1 2024-07-11       10      open        
#>  2 2024-07-08       09      open        
#>  3 2024-02-09       08      open        
#>  4 2023-12-14       07      open        
#>  5 2023-12-12       06      open        
#>  6 2023-09-14       05      open        
#>  7 2023-07-26       04      open        
#>  8 2023-06-14       03      open        
#>  9 2023-05-24       02      open        
#> 10 2022-12-02       01      restricted  
# }
```
