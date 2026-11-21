# Tibble Summary for Vintages Data

Provides the custom header shown when a vintages object is printed. This
method is called automatically by pillar. It is defined once for the
parent class
[tbl_vintage](https://docs.ropensci.org/reviser/reference/tbl_vintage.md)
and inherited by `tbl_pubdate` and `tbl_release` objects alike, so that
both report the same fields.

## Usage

``` r
# S3 method for class 'tbl_vintage'
tbl_sum(x, ...)
```

## Arguments

- x:

  An object inheriting from
  [tbl_vintage](https://docs.ropensci.org/reviser/reference/tbl_vintage.md),
  such as a `tbl_pubdate` or a `tbl_release`.

- ...:

  Additional arguments (unused).

## Value

A named character vector where names are labels and values are the
corresponding information. The vector is used by pillar to format the
tibble header. An object whose columns no longer match either documented
layout falls back to the plain tibble header, so that a broken object
can still be inspected;
[`summary()`](https://rdrr.io/r/base/summary.html) reports the problem.

## See also

Other helpers:
[`print.tbl_vintage()`](https://docs.ropensci.org/reviser/reference/print.tbl_vintage.md),
[`summary.tbl_vintage()`](https://docs.ropensci.org/reviser/reference/summary.tbl_vintage.md),
[`tbl_vintage`](https://docs.ropensci.org/reviser/reference/tbl_vintage.md),
[`validate_vintages()`](https://docs.ropensci.org/reviser/reference/validate_vintages.md),
[`vintages_long()`](https://docs.ropensci.org/reviser/reference/vintages_long.md),
[`vintages_wide()`](https://docs.ropensci.org/reviser/reference/vintages_wide.md)

## Examples

``` r
df <- dplyr::filter(reviser::gdp, id == "US")
release_data <- get_nth_release(df, n = 0:3)
pillar::tbl_sum(release_data)
#> Vintages data (release format)                         Format 
#>                             ""                         "long" 
#>                   Time periods                       Releases 
#>                          "179"                            "4" 
#>                            IDs 
#>                            "1" 
```
