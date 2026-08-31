# Forecasts from a Revision Model

Returns the out-of-sample estimates of the model's latent signal
produced by the forecast horizon `h` supplied to
[`kk_nowcast()`](https://docs.ropensci.org/reviser/reference/kk_nowcast.md)
or
[`jvn_nowcast()`](https://docs.ropensci.org/reviser/reference/jvn_nowcast.md).
The horizon is fixed at estimation time, so refit with a different `h`
to change it.

## Usage

``` r
# S3 method for class 'revision_model'
predict(object, ...)
```

## Arguments

- object:

  A fitted model object inheriting from
  [revision_model](https://docs.ropensci.org/reviser/reference/revision_model.md),
  such as a `kk_model` or a `jvn_model`.

- ...:

  Ignored.

## Value

A tibble with columns `time`, `estimate`, `lower` and `upper`. Has zero
rows when the model was fitted with `h = 0`.

## See also

Other revision nowcasting:
[`coef.revision_model()`](https://docs.ropensci.org/reviser/reference/coef.revision_model.md),
[`fitted.revision_model()`](https://docs.ropensci.org/reviser/reference/fitted.revision_model.md),
[`jvn_nowcast()`](https://docs.ropensci.org/reviser/reference/jvn_nowcast.md),
[`kk_nowcast()`](https://docs.ropensci.org/reviser/reference/kk_nowcast.md),
[`logLik.revision_model()`](https://docs.ropensci.org/reviser/reference/logLik.revision_model.md),
[`nobs.revision_model()`](https://docs.ropensci.org/reviser/reference/nobs.revision_model.md),
[`plot.revision_model()`](https://docs.ropensci.org/reviser/reference/plot.revision_model.md),
[`print.revision_model()`](https://docs.ropensci.org/reviser/reference/print.revision_model.md),
[`residuals.revision_model()`](https://docs.ropensci.org/reviser/reference/residuals.revision_model.md),
[`revision_model`](https://docs.ropensci.org/reviser/reference/revision_model.md),
[`states()`](https://docs.ropensci.org/reviser/reference/states.md),
[`summary.revision_model()`](https://docs.ropensci.org/reviser/reference/summary.revision_model.md),
[`vcov.revision_model()`](https://docs.ropensci.org/reviser/reference/vcov.revision_model.md)

## Examples

``` r
df <- get_nth_release(
  tsbox::ts_span(
    tsbox::ts_pc(dplyr::filter(reviser::gdp, id == "US")),
    start = "1980-01-01"
  ),
  n = 0:1
)
df <- na.omit(dplyr::select(df, -c("id", "pub_date")))
fit <- kk_nowcast(df, e = 1, h = 2, model = "KK", method = "MLE")
predict(fit)
#> # A tibble: 2 × 4
#>   time       estimate lower upper
#>   <date>        <dbl> <dbl> <dbl>
#> 1 2024-10-01   0.144  -2.33  2.62
#> 2 2025-01-01   0.0286 -2.50  2.55
```
