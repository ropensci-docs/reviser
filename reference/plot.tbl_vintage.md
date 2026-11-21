# Plot Method for Vintages Data

Plots a vintages object along the dimension implied by its class:
publication date for a `tbl_pubdate`, release number for a
`tbl_release`. Defined once for the parent class
[tbl_vintage](https://docs.ropensci.org/reviser/reference/tbl_vintage.md)
and inherited by both.
[`plot_vintages()`](https://docs.ropensci.org/reviser/reference/plot_vintages.md)
remains the entry point when the dimension, title or plot type need to
be set explicitly.

## Usage

``` r
# S3 method for class 'tbl_vintage'
plot(x, ...)
```

## Arguments

- x:

  An object inheriting from
  [tbl_vintage](https://docs.ropensci.org/reviser/reference/tbl_vintage.md),
  such as a `tbl_pubdate` or a `tbl_release`.

- ...:

  Additional arguments passed to
  [`plot_vintages()`](https://docs.ropensci.org/reviser/reference/plot_vintages.md).

## Value

A ggplot2 object.

## See also

Other revision graphs:
[`plot_vintages()`](https://docs.ropensci.org/reviser/reference/plot_vintages.md),
[`theme_reviser()`](https://docs.ropensci.org/reviser/reference/theme_reviser.md)

## Examples

``` r
df <- dplyr::filter(reviser::gdp, id == "US")
plot(df)
#> Warning: 89 time series supplied. Showing recent 30.


release_data <- get_nth_release(df, n = 0:5)
plot(release_data)
```
