# Vintages Data Objects

`reviser` represents real-time vintages as tibbles that carry an
additional class recording which dimension indexes the vintages. Data
indexed by publication date are of class `tbl_pubdate`, data indexed by
release number are of class `tbl_release`, and both inherit from the
common parent class `tbl_vintage`, ahead of the usual tibble classes. A
fitted class attribute therefore reads
`c("tbl_pubdate", "tbl_vintage", "tbl_df", "tbl", "data.frame")`. An
object that carries both a `pub_date` and a `release` column is classed
as both, with `tbl_release` taking precedence.

The parent class holds everything the two representations share. The
[`print()`](https://rdrr.io/r/base/print.html),
[`summary()`](https://rdrr.io/r/base/summary.html),
[`plot()`](https://rdrr.io/r/graphics/plot.default.html) and
[`pillar::tbl_sum()`](https://pillar.r-lib.org/reference/tbl_sum.html)
methods are defined once for `tbl_vintage` and inherited by both, so
that the two stay consistent with one another. Only the parts that
genuinely depend on the indexing dimension are dispatched on the child
classes, through the internal generics `vintage_labels()`,
`vintage_value_cols()` and `vintage_detail()`.

Both representations may be stored in either a long or a wide layout,
and the methods below detect which and report accordingly. The layouts,
and the columns each one requires, are specified under "Data contract"
in
[`validate_vintages()`](https://docs.ropensci.org/reviser/reference/validate_vintages.md),
which also checks an object against them. Use
[`vintages_long()`](https://docs.ropensci.org/reviser/reference/vintages_long.md)
and
[`vintages_wide()`](https://docs.ropensci.org/reviser/reference/vintages_wide.md)
to convert between layouts.

## Value

This topic documents a class rather than a function. The functions that
build vintages data, such as
[`get_nth_release()`](https://docs.ropensci.org/reviser/reference/get_nth_release.md),
[`vintages_long()`](https://docs.ropensci.org/reviser/reference/vintages_long.md)
and
[`vintages_wide()`](https://docs.ropensci.org/reviser/reference/vintages_wide.md),
return tibbles whose class attribute is
`c("tbl_pubdate", "tbl_vintage", "tbl_df", "tbl", "data.frame")` or the
same with `"tbl_release"` in place of `"tbl_pubdate"`.

## See also

[`validate_vintages()`](https://docs.ropensci.org/reviser/reference/validate_vintages.md),
[`vintages_long()`](https://docs.ropensci.org/reviser/reference/vintages_long.md),
[`vintages_wide()`](https://docs.ropensci.org/reviser/reference/vintages_wide.md)

Other helpers:
[`print.tbl_vintage()`](https://docs.ropensci.org/reviser/reference/print.tbl_vintage.md),
[`summary.tbl_vintage()`](https://docs.ropensci.org/reviser/reference/summary.tbl_vintage.md),
[`tbl_sum.tbl_vintage()`](https://docs.ropensci.org/reviser/reference/tbl_sum.tbl_vintage.md),
[`validate_vintages()`](https://docs.ropensci.org/reviser/reference/validate_vintages.md),
[`vintages_long()`](https://docs.ropensci.org/reviser/reference/vintages_long.md),
[`vintages_wide()`](https://docs.ropensci.org/reviser/reference/vintages_wide.md)

## Examples

``` r
df <- dplyr::filter(reviser::gdp, id == "US")

# Release vintages carry the shared parent class.
releases <- get_nth_release(df, n = 0:3)
class(releases)
#> [1] "tbl_release" "tbl_pubdate" "tbl_vintage" "tbl_df"      "tbl"        
#> [6] "data.frame" 
inherits(releases, "tbl_vintage")
#> [1] TRUE

# So do publication-date vintages, in either layout.
class(vintages_wide(df)$US)
#> [1] "tbl_pubdate" "tbl_vintage" "tbl_df"      "tbl"         "data.frame" 

# The print, summary and plot methods are inherited from the parent.
summary(releases)
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
```
