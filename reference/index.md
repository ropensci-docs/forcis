# Package index

## Database tools

Functions to download and import FORCIS database

- [`download_forcis_db()`](https://docs.ropensci.org/forcis/reference/download_forcis_db.md)
  : Download the FORCIS database
- [`read_cpr_north_data()`](https://docs.ropensci.org/forcis/reference/read_data.md)
  [`read_cpr_south_data()`](https://docs.ropensci.org/forcis/reference/read_data.md)
  [`read_plankton_nets_data()`](https://docs.ropensci.org/forcis/reference/read_data.md)
  [`read_pump_data()`](https://docs.ropensci.org/forcis/reference/read_data.md)
  [`read_sediment_trap_data()`](https://docs.ropensci.org/forcis/reference/read_data.md)
  : Read FORCIS data

## Database versions

Functions to get information on database versions

- [`get_available_versions()`](https://docs.ropensci.org/forcis/reference/get_available_versions.md)
  : Get available versions of the FORCIS database
- [`get_version_metadata()`](https://docs.ropensci.org/forcis/reference/get_version_metadata.md)
  : Print information of a specific version of the FORCIS database

## Select and filters tools

Function to select and filter FORCIS data

- [`select_forcis_columns()`](https://docs.ropensci.org/forcis/reference/select_forcis_columns.md)
  : Select columns in FORCIS data
- [`select_taxonomy()`](https://docs.ropensci.org/forcis/reference/select_taxonomy.md)
  : Select a taxonomy in FORCIS data
- [`filter_by_species()`](https://docs.ropensci.org/forcis/reference/filter_by_species.md)
  : Filter FORCIS data by species
- [`filter_by_month()`](https://docs.ropensci.org/forcis/reference/filter_by_month.md)
  : Filter FORCIS data by month of sampling
- [`filter_by_year()`](https://docs.ropensci.org/forcis/reference/filter_by_year.md)
  : Filter FORCIS data by year of sampling
- [`filter_by_bbox()`](https://docs.ropensci.org/forcis/reference/filter_by_bbox.md)
  : Filter FORCIS data by a spatial bounding box
- [`filter_by_ocean()`](https://docs.ropensci.org/forcis/reference/filter_by_ocean.md)
  : Filter FORCIS data by ocean
- [`filter_by_polygon()`](https://docs.ropensci.org/forcis/reference/filter_by_polygon.md)
  : Filter FORCIS data by a spatial polygon

## Standardization functions

Functions to homogenize, compute, and aggregate FORCIS data

- [`compute_abundances()`](https://docs.ropensci.org/forcis/reference/computations.md)
  [`compute_concentrations()`](https://docs.ropensci.org/forcis/reference/computations.md)
  [`compute_frequencies()`](https://docs.ropensci.org/forcis/reference/computations.md)
  : Compute count conversions

## Visualization tools

Functions to visualize FORCIS data

- [`geom_basemap()`](https://docs.ropensci.org/forcis/reference/geom_basemap.md)
  : Add a World basemap to a ggplot object
- [`ggmap_data()`](https://docs.ropensci.org/forcis/reference/ggmap_data.md)
  : Map the spatial distribution of FORCIS data
- [`plot_record_by_year()`](https://docs.ropensci.org/forcis/reference/plot_record_by_year.md)
  : Plot sample records by year
- [`plot_record_by_month()`](https://docs.ropensci.org/forcis/reference/plot_record_by_month.md)
  : Plot sample records by month
- [`plot_record_by_season()`](https://docs.ropensci.org/forcis/reference/plot_record_by_season.md)
  : Plot sample records by season
- [`plot_record_by_depth()`](https://docs.ropensci.org/forcis/reference/plot_record_by_depth.md)
  : Plot sample records by depth of collection

## Utilities

Helper functions

- [`convert_to_long_format()`](https://docs.ropensci.org/forcis/reference/convert_to_long_format.md)
  : Reshape and simplify FORCIS data
- [`data_to_sf()`](https://docs.ropensci.org/forcis/reference/data_to_sf.md)
  : Convert a data frame into an sf object
- [`get_ocean_names()`](https://docs.ropensci.org/forcis/reference/get_ocean_names.md)
  : Get World ocean names
- [`get_required_columns()`](https://docs.ropensci.org/forcis/reference/get_required_columns.md)
  : Get required column names
- [`get_species_names()`](https://docs.ropensci.org/forcis/reference/get_species_names.md)
  : Get species names from column names
