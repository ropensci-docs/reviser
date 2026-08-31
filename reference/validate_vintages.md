# Vintages Data Classes and Their Validation

`reviser` stores vintages in two S3 classes that sit on top of a tibble
and record what the columns mean. Both are produced by the package's own
constructors; you normally do not create them by hand.

- `tbl_pubdate`:

  Vintages identified by publication date, as returned by
  [`vintages_wide()`](https://docs.ropensci.org/reviser/reference/vintages_wide.md),
  [`vintages_long()`](https://docs.ropensci.org/reviser/reference/vintages_long.md)
  and
  [`get_revisions()`](https://docs.ropensci.org/reviser/reference/get_revisions.md).

- `tbl_release`:

  Vintages identified by release number, as returned by
  [`get_first_release()`](https://docs.ropensci.org/reviser/reference/get_first_release.md),
  [`get_nth_release()`](https://docs.ropensci.org/reviser/reference/get_nth_release.md),
  [`get_latest_release()`](https://docs.ropensci.org/reviser/reference/get_latest_release.md),
  [`get_fixed_release()`](https://docs.ropensci.org/reviser/reference/get_fixed_release.md)
  and
  [`get_releases_by_date()`](https://docs.ropensci.org/reviser/reference/get_releases_by_date.md).

`validate_vintages()` checks that an object conforms to the contract
below. This is useful after manipulating a vintages object with external
tools, which can leave the class attribute in place while breaking the
assumptions the methods rely on.

## Usage

``` r
validate_vintages(x)
```

## Arguments

- x:

  An object of class `tbl_pubdate` or `tbl_release`.

## Value

`x`, invisibly, if it is valid. Otherwise an error describing the first
problem found.

## Data contract

Every object of either class has a `time` column of dates and may carry
an optional `id` column identifying the series. Beyond that, each class
has two permitted layouts:

- long:

  A key column (`pub_date` for `tbl_pubdate`, `release` for
  `tbl_release`) together with a `value` column.

- wide:

  One column per vintage. For `tbl_pubdate` the column names are
  publication dates in `%Y-%m-%d` form; for `tbl_release` they are
  release labels matching `release` or `final`.

Columns must be atomic and scalar-valued; list columns are not
permitted. The two classes are not mutually exclusive: a long release
table carries both a `release` and a `pub_date` column and holds both
classes, with `tbl_release` taking precedence for method dispatch.

A valid object also inherits from the shared parent class
[tbl_vintage](https://docs.ropensci.org/reviser/reference/tbl_vintage.md),
which is where its methods live; `validate_vintages()` checks for that
too. See
[tbl_vintage](https://docs.ropensci.org/reviser/reference/tbl_vintage.md)
for the class hierarchy and the methods it provides.

## Operations that drop the class

The vintages classes sit on top of a tibble, so the `dplyr` verbs
([`filter()`](https://dplyr.tidyverse.org/reference/filter.html),
[`mutate()`](https://dplyr.tidyverse.org/reference/mutate.html),
[`select()`](https://dplyr.tidyverse.org/reference/select.html),
[`arrange()`](https://dplyr.tidyverse.org/reference/arrange.html),
[`slice()`](https://dplyr.tidyverse.org/reference/slice.html)) and `[`
preserve them. A few functions rebuild the object from scratch and
return a plain tibble instead;
[`tidyr::drop_na()`](https://tidyr.tidyverse.org/reference/drop_na.html)
is the one most likely to be met in a vintages workflow. The data are
unaffected, but
[`plot()`](https://rdrr.io/r/graphics/plot.default.html),
[`summary()`](https://rdrr.io/r/base/summary.html) and the vintages
print header no longer dispatch. Pass the result back through
[`vintages_long()`](https://docs.ropensci.org/reviser/reference/vintages_long.md)
or
[`vintages_wide()`](https://docs.ropensci.org/reviser/reference/vintages_wide.md),
or apply the operation before the release-extraction step, to get the
class back.

## See also

Other helpers:
[`print.tbl_vintage()`](https://docs.ropensci.org/reviser/reference/print.tbl_vintage.md),
[`summary.tbl_vintage()`](https://docs.ropensci.org/reviser/reference/summary.tbl_vintage.md),
[`tbl_sum.tbl_vintage()`](https://docs.ropensci.org/reviser/reference/tbl_sum.tbl_vintage.md),
[`tbl_vintage`](https://docs.ropensci.org/reviser/reference/tbl_vintage.md),
[`vintages_long()`](https://docs.ropensci.org/reviser/reference/vintages_long.md),
[`vintages_wide()`](https://docs.ropensci.org/reviser/reference/vintages_wide.md)

## Examples

``` r
df <- dplyr::filter(reviser::gdp, id == "US")

releases <- get_nth_release(df, n = 0:3)
validate_vintages(releases)

# A malformed time column is rejected
broken <- releases
broken$time <- as.character(broken$time)
broken$time[1] <- "not a date"
try(validate_vintages(broken))
#> Error in validate_vintages(broken) : 
#>   The 'time' column must contain dates in '%Y-%m-%d' format.

# So is a class attribute that contradicts the columns
mislabelled <- vintages_wide(df)$US
class(mislabelled) <- c("tbl_release", class(mislabelled))
try(validate_vintages(mislabelled))
#> Error in validate_vintages(mislabelled) : 
#>   Object is classed as 'tbl_release', so it must have a 'release' column (long format) or release labels as column names (wide format).
```
