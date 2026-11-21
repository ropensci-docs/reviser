# Extract the Latent State Estimates of a Revision Model

Accessor for the state paths of a fitted revision-nowcasting model.
Provides programmatic access to the estimated states instead of reaching
into the object with `fit$states`. The method is defined once for the
parent class
[revision_model](https://docs.ropensci.org/reviser/reference/revision_model.md)
and is inherited by `kk_model` and `jvn_model` objects alike.

## Usage

``` r
states(object, ...)

# S3 method for class 'revision_model'
states(object, filter = c("smoothed", "filtered", "all"), state = NULL, ...)
```

## Arguments

- object:

  A fitted model object inheriting from
  [revision_model](https://docs.ropensci.org/reviser/reference/revision_model.md),
  such as a `kk_model` or a `jvn_model`.

- ...:

  Additional arguments passed to methods.

- filter:

  Which state estimates to return: `"smoothed"` (default) uses the full
  sample, `"filtered"` uses information available up to each date, and
  `"all"` returns both.

- state:

  Optional character vector of state names to keep. Defaults to all
  states.

## Value

A tibble with columns `time`, `state`, `estimate`, `lower`, `upper`,
`filter` and `sample`.

## See also

Other revision nowcasting:
[`coef.revision_model()`](https://docs.ropensci.org/reviser/reference/coef.revision_model.md),
[`fitted.revision_model()`](https://docs.ropensci.org/reviser/reference/fitted.revision_model.md),
[`jvn_nowcast()`](https://docs.ropensci.org/reviser/reference/jvn_nowcast.md),
[`kk_nowcast()`](https://docs.ropensci.org/reviser/reference/kk_nowcast.md),
[`logLik.revision_model()`](https://docs.ropensci.org/reviser/reference/logLik.revision_model.md),
[`nobs.revision_model()`](https://docs.ropensci.org/reviser/reference/nobs.revision_model.md),
[`plot.revision_model()`](https://docs.ropensci.org/reviser/reference/plot.revision_model.md),
[`predict.revision_model()`](https://docs.ropensci.org/reviser/reference/predict.revision_model.md),
[`print.revision_model()`](https://docs.ropensci.org/reviser/reference/print.revision_model.md),
[`residuals.revision_model()`](https://docs.ropensci.org/reviser/reference/residuals.revision_model.md),
[`revision_model`](https://docs.ropensci.org/reviser/reference/revision_model.md),
[`summary.revision_model()`](https://docs.ropensci.org/reviser/reference/summary.revision_model.md),
[`vcov.revision_model()`](https://docs.ropensci.org/reviser/reference/vcov.revision_model.md)

## Examples

``` r
# \donttest{
gdp_growth <- dplyr::filter(
  tsbox::ts_pc(reviser::gdp),
  id == "EA",
  time >= min(pub_date),
  time <= as.Date("2020-01-01")
)
gdp_growth <- tidyr::drop_na(gdp_growth)
df <- get_nth_release(gdp_growth, n = 0:3)

fit <- jvn_nowcast(df = df, e = 4, ar_order = 2, include_noise = FALSE)
head(states(fit))
#> # A tibble: 6 × 7
#>   time       state      estimate     lower   upper filter   sample   
#>   <date>     <chr>         <dbl>     <dbl>   <dbl> <chr>    <chr>    
#> 1 2002-10-01 news_vint1   0.112   0.0141    0.210  smoothed in_sample
#> 2 2003-01-01 news_vint1   0.0212 -0.0766    0.119  smoothed in_sample
#> 3 2003-04-01 news_vint1   0.0983  0.000530  0.196  smoothed in_sample
#> 4 2003-07-01 news_vint1  -0.0774 -0.175     0.0204 smoothed in_sample
#> 5 2003-10-01 news_vint1  -0.153  -0.251    -0.0555 smoothed in_sample
#> 6 2004-01-01 news_vint1  -0.185  -0.283    -0.0876 smoothed in_sample
head(states(fit, filter = "filtered", state = "true_lag_0"))
#> # A tibble: 6 × 7
#>   time       state      estimate   lower   upper filter   sample   
#>   <date>     <chr>         <dbl>   <dbl>   <dbl> <chr>    <chr>    
#> 1 2002-10-01 true_lag_0  0.0577  -0.0403 0.156   filtered in_sample
#> 2 2003-01-01 true_lag_0 -0.00601 -0.104  0.0920  filtered in_sample
#> 3 2003-04-01 true_lag_0 -0.0957  -0.194  0.00226 filtered in_sample
#> 4 2003-07-01 true_lag_0  0.461    0.363  0.559   filtered in_sample
#> 5 2003-10-01 true_lag_0  0.465    0.367  0.563   filtered in_sample
#> 6 2004-01-01 true_lag_0  0.758    0.660  0.856   filtered in_sample
# }
```
