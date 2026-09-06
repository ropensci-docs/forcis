# Get World ocean names

This function returns the name of World oceans according to the IHO Sea
Areas dataset version 3 (Flanders Marine Institute, 2018).

## Usage

``` r
get_ocean_names()
```

## Value

A `character` vector with World ocean names.

## References

Flanders Marine Institute (2018). IHO Sea Areas, version 3. Available
online at: <https://www.marineregions.org/>. DOI:
[doi:10.14284/323](https://doi.org/10.14284/323) .

## Examples

``` r
# Print the name of World oceans ----
get_ocean_names()
#> [1] "Arctic Ocean"         "Indian Ocean"         "Mediterranean Sea"   
#> [4] "North Atlantic Ocean" "North Pacific Ocean"  "South Atlantic Ocean"
#> [7] "South Pacific Ocean"  "Southern Ocean"      
```
