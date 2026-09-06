# Reshape and simplify FORCIS data

Reshapes FORCIS data by pivoting species columns into two columns:
`taxa` (taxon names) and `counts` (taxon abundances). It converts wider
`data.frame` to a long format.

## Usage

``` r
convert_to_long_format(data)
```

## Arguments

- data:

  a `tibble` or a `data.frame`, i.e. a FORCIS dataset, except for CPR
  North data.

## Value

A `tibble` reshaped in a long format.

## Examples

``` r
# Import example dataset ----
file_name <- system.file(file.path("extdata", "FORCIS_net_sample.csv"),
                         package = "forcis")

net_data <- read.csv(file_name)

# Dimensions of the data.frame ----
dim(net_data)
#> [1] 2451   86

# Reshape data ----
net_data <- convert_to_long_format(net_data)

# Dimensions of the data.frame ----
dim(net_data)
#> [1] 151962     23

# Column names ----
colnames(net_data)
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
