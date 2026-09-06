# Get required column names

Gets required column names (except taxa names) for the package. This
function is designed to help users to add additional columns in
[`select_forcis_columns()`](https://docs.ropensci.org/forcis/reference/select_forcis_columns.md)
(argument `cols`) if missing from this list.

These columns are required by some functions (`compute_*()`, `plot_*()`,
etc.) of the package and shouldn't be deleted.

## Usage

``` r
get_required_columns()
```

## Value

A `character` vector.

## Examples

``` r
# Get required column names (expect taxa names) ----
get_required_columns()
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
```
