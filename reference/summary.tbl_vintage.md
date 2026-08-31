# Summary Method for Vintages Data

Reports the layout, time coverage, number of vintages and missing-value
count of a vintages object. Defined once for the parent class
[tbl_vintage](https://docs.ropensci.org/reviser/reference/tbl_vintage.md);
the block describing the vintages themselves is supplied by the concrete
class.

## Usage

``` r
# S3 method for class 'tbl_vintage'
summary(object, ...)
```

## Arguments

- object:

  An object inheriting from
  [tbl_vintage](https://docs.ropensci.org/reviser/reference/tbl_vintage.md),
  such as a `tbl_pubdate` or a `tbl_release`.

- ...:

  Additional arguments (not used).

## Value

The input `object`, invisibly.

## See also

Other helpers:
[`print.tbl_vintage()`](https://docs.ropensci.org/reviser/reference/print.tbl_vintage.md),
[`tbl_sum.tbl_vintage()`](https://docs.ropensci.org/reviser/reference/tbl_sum.tbl_vintage.md),
[`tbl_vintage`](https://docs.ropensci.org/reviser/reference/tbl_vintage.md),
[`validate_vintages()`](https://docs.ropensci.org/reviser/reference/validate_vintages.md),
[`vintages_long()`](https://docs.ropensci.org/reviser/reference/vintages_long.md),
[`vintages_wide()`](https://docs.ropensci.org/reviser/reference/vintages_wide.md)

## Examples

``` r
df <- dplyr::filter(reviser::gdp, id == "US")

# Long format
release_data <- get_nth_release(df, n = 0:3)
summary(release_data)
#> 
#> === Vintages Data Summary (Release Format) ===
#> 
#> Format: long 
#> Time periods: 179 
#> Time range: 1980-01-01 to 2024-07-01 
#> Number of IDs: 1 
#> IDs: US 
#> 
#> Number of releases: 4 
#> Releases: release_0, release_1, release_2, release_3 
#> 
#> Missing values: 0 of 710 (0%) 

# Wide format
wide_release <- vintages_wide(release_data, names_from = "release")
#> Warning: Ignoring columns: pub_date
summary(wide_release$US)
#> 
#> === Vintages Data Summary (Release Format) ===
#> 
#> Format: wide 
#> Time periods: 179 
#> Time range: 1980-01-01 to 2024-07-01 
#> 
#> Number of releases: 4 
#> Releases: release_0, release_1, release_2, release_3 
#> 
#> Missing values: 6 of 716 (0.84%) 

# Publication-date vintages
summary(vintages_wide(df)$US)
#> 
#> === Vintages Data Summary (Publication Date Format) ===
#> 
#> Format: wide 
#> Time periods: 179 
#> Time range: 1980-01-01 to 2024-07-01 
#> 
#> Number of vintages: 89 
#> Publication dates: 
#>   Earliest: 2002-10-01 
#>   Latest: 2024-10-01 
#> 
#> Missing values: 3916 of 15931 (24.58%) 
```
