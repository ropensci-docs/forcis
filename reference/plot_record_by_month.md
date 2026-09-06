# Plot sample records by month

This function produces a barplot of FORCIS sample records by month.

## Usage

``` r
plot_record_by_month(data)
```

## Arguments

- data:

  a `tibble` or a `data.frame`, i.e. a FORCIS dataset.

## Value

A `ggplot` object.

## Examples

``` r
# Import example dataset ----
file_name <- system.file(file.path("extdata", "FORCIS_net_sample.csv"),
                         package = "forcis")

net_data <- read.csv(file_name)

# Plot data by year (example dataset) ----
plot_record_by_month(net_data)
```
