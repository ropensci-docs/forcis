# Get species names from column names

Gets species names from column names. This function is just an utility
to easily retrieve taxon names.

## Usage

``` r
get_species_names(data)
```

## Arguments

- data:

  a `tibble` or a `data.frame`. One obtained by `read_*_data()`
  functions.

## Value

A `character` vector of species names.

## Examples

``` r
# Import example dataset ----
file_name <- system.file(file.path("extdata", "FORCIS_net_sample.csv"),
                         package = "forcis")

net_data <- read.csv(file_name)

# Select a taxonomy ----
net_data <- select_taxonomy(net_data, taxonomy = "VT")

# Retrieve taxon names ----
get_species_names(net_data)
#>  [1] "b_digitata_VT"                 "b_pumilio_VT"                 
#>  [3] "b_variabilis_VT"               "c_nitida_VT"                  
#>  [5] "d_anfracta_VT"                 "g_adamsi_VT"                  
#>  [7] "g_bulloides_VT"                "g_calida_VT"                  
#>  [9] "g_cavernula_VT"                "g_conglobatus_VT"             
#> [11] "g_conglomerata_VT"             "g_crassaformis_VT"            
#> [13] "g_elongatus_VT"                "g_falconensis_VT"             
#> [15] "g_glutinata_VT"                "g_hexagona_VT"                
#> [17] "g_hirsuta_VT"                  "g_inflata_VT"                 
#> [19] "g_cultrata_VT"                 "g_minuta_VT"                  
#> [21] "g_ruber_albus_VT"              "g_ruber_albus_or_elongatus_VT"
#> [23] "g_ruber_any_VT"                "g_ruber_ruber_VT"             
#> [25] "g_rubescens_VT"                "g_scitula_VT"                 
#> [27] "g_siphonifera_VT"              "g_tenellus_VT"                
#> [29] "g_theyeri_VT"                  "g_truncatulinoides_VT"        
#> [31] "g_truncatulinoides_left_VT"    "g_truncatulinoides_right_VT"  
#> [33] "g_tumida_VT"                   "g_ungulata_VT"                
#> [35] "g_uvula_VT"                    "n_vivans_VT"                  
#> [37] "h_digitata_VT"                 "h_pelagica_VT"                
#> [39] "n_dutertrei_VT"                "n_incompta_VT"                
#> [41] "n_pachyderma_VT"               "n_pachyderma_incompta_VT"     
#> [43] "o_riedeli_VT"                  "o_universa_VT"                
#> [45] "p_obliquiloculata_VT"          "s_dehiscens_VT"               
#> [47] "t_clarkei_VT"                  "t_fleisheri_VT"               
#> [49] "t_humilis_VT"                  "t_iota_VT"                    
#> [51] "t_parkerae_VT"                 "t_quinqueloba_VT"             
#> [53] "t_sacculifer_VT"               "t_sacculifer_no_sac_VT"       
#> [55] "t_sacculifer_sac_VT"           "UnID_VT"                      
```
