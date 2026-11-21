# Vintages Data

A collection of real-time datasets.

## Usage

``` r
gdp
```

## Format

A `tbl_pubdate` vintages object in the long layout: a tibble carrying
the class attribute
`c("tbl_pubdate", "tbl_vintage", "tbl_df", "tbl", "data.frame")`, with
quarterly observations and 4 variables:

- time:

  Date of the observation

- pub_date:

  Publication date of the vintage

- value:

  Numeric, real GDP (seasonally adjusted)

- id:

  Country code

Because it is a vintages object rather than a plain tibble, the generics
[`print()`](https://rdrr.io/r/base/print.html),
[`summary()`](https://rdrr.io/r/base/summary.html) and
[`plot()`](https://rdrr.io/r/graphics/plot.default.html) work on it
directly. See
[`validate_vintages()`](https://docs.ropensci.org/reviser/reference/validate_vintages.md)
for the data contract and
[tbl_vintage](https://docs.ropensci.org/reviser/reference/tbl_vintage.md)
for the class hierarchy.

## Details

- GDP: Quarterly Vintages (Billions of real dollars, seasonally
  adjusted)

- Timeframe: Q1 1980 - Q4 2024

- Real-Time Vintages: Q4 2002 - Q4 2024

## Sources

- All the data is from the realtime database of Indergand and Leist
  (2014). **Countries**:

- CHE:

  - Switzerland

  - Source: SECO

- US:

  - United States

  - Sources: FRED, OECD

- EA:

  - Euro Area

  - Sources: Eurostat, OECD

- JP:

  - Japan

  - Sources: Cabinet Office (Japan), OECD

## References

Indergand, R., Leist, S. A Real-Time Data Set for Switzerland. Swiss J
Economics Statistics 150, 331–352 (2014).
[doi:10.1007/BF03399410](https://doi.org/10.1007/BF03399410)

## See also

[`validate_vintages()`](https://docs.ropensci.org/reviser/reference/validate_vintages.md),
[tbl_vintage](https://docs.ropensci.org/reviser/reference/tbl_vintage.md)

## Examples

``` r
# Load gdp dataset
data(gdp)
head(gdp)
#> # Vintages data (publication date format):
#> # Format:                                  long
#> # Time periods:                            1
#> # Vintages:                                6
#> # IDs:                                     1
#>   time       pub_date    value id   
#>   <date>     <date>      <dbl> <chr>
#> 1 1980-01-01 2002-10-01 64551. CHE  
#> 2 1980-01-01 2003-01-01 64551. CHE  
#> 3 1980-01-01 2003-04-01 64556. CHE  
#> 4 1980-01-01 2003-07-01 64551. CHE  
#> 5 1980-01-01 2003-10-01 64551. CHE  
#> 6 1980-01-01 2004-04-01 75004. CHE  

# It is a vintages object, so the generics dispatch on it directly.
class(gdp)
#> [1] "tbl_pubdate" "tbl_vintage" "tbl_df"      "tbl"         "data.frame" 
summary(gdp)
#> 
#> === Vintages Data Summary (Publication Date Format) ===
#> 
#> Format: long 
#> Time periods: 179 
#> Time range: 1980-01-01 to 2024-07-01 
#> Number of IDs: 4 
#> IDs: CHE, US, JP, EA 
#> 
#> Number of vintages: 89 
#> Publication dates: 
#>   Earliest: 2002-10-01 
#>   Latest: 2024-10-01 
#> 
#> Missing values: 0 of 47980 (0%) 
```
