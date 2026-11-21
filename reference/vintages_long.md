# Convert Vintages Data to Long Format

Converts a vintages dataset from wide format to long format, optionally
adding `id` if the input is a list of data frames. The long format
contains one row per combination of `time` and `names_to` (e.g.,
`pub_date` or `release`), with values stored in a single `value` column.

## Usage

``` r
vintages_long(df, names_to = "pub_date", keep_na = FALSE)
```

## Arguments

- df:

  A data frame, tibble, or list of data frames containing vintages data
  in wide format.

- names_to:

  The name of the column to create from the wide-format column names.
  Must be either `"pub_date"` (default) or `"release"`.

- keep_na:

  Logical. If `TRUE`, retains rows with `NA` values in the `value`
  column. Default is `FALSE`.

## Value

A long-format vintages object: a tibble carrying the `tbl_pubdate` or
`tbl_release` class and their shared parent
[tbl_vintage](https://docs.ropensci.org/reviser/reference/tbl_vintage.md).
If the input is a list of wide-format data frames, the output is a
single combined long-format object.

Long-format input is returned with the vintages class attached, which is
also how to recover the class after an operation that dropped it (see
the "Operations that drop the class" section of
[`validate_vintages()`](https://docs.ropensci.org/reviser/reference/validate_vintages.md)).
Input that is already a long-format vintages object warns, because the
call is then a no-op.

## See also

Other helpers:
[`print.tbl_vintage()`](https://docs.ropensci.org/reviser/reference/print.tbl_vintage.md),
[`summary.tbl_vintage()`](https://docs.ropensci.org/reviser/reference/summary.tbl_vintage.md),
[`tbl_sum.tbl_vintage()`](https://docs.ropensci.org/reviser/reference/tbl_sum.tbl_vintage.md),
[`tbl_vintage`](https://docs.ropensci.org/reviser/reference/tbl_vintage.md),
[`validate_vintages()`](https://docs.ropensci.org/reviser/reference/validate_vintages.md),
[`vintages_wide()`](https://docs.ropensci.org/reviser/reference/vintages_wide.md)

## Examples

``` r
# Example wide-format data
long_data <- dplyr::filter(reviser::gdp, id == "US")

# Convert to wide format
wide_data <- vintages_wide(long_data)

# Example list of wide-format data frames
wide_list <- list(
  A = wide_data$US,
  B = wide_data$US
)

# Convert list to long format
long_data <- vintages_long(wide_list, names_to = "pub_date")
```
