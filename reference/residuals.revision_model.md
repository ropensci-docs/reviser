# Residuals of a Revision Model

Difference between the observed target release and the smoothed estimate
of the model's latent signal. These are measurement residuals of the
release the model treats as its target – the efficient release for a
`kk_model`, the most mature release included in the estimation for a
`jvn_model` – not one-step-ahead prediction errors.

## Usage

``` r
# S3 method for class 'revision_model'
residuals(object, ...)
```

## Arguments

- object:

  A fitted model object inheriting from
  [revision_model](https://docs.ropensci.org/reviser/reference/revision_model.md),
  such as a `kk_model` or a `jvn_model`.

- ...:

  Ignored.

## Value

A tibble with columns `time` and `residual`.

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
fit <- kk_nowcast(df, e = 1, model = "KK", method = "MLE")
head(residuals(fit))
#> # A tibble: 6 × 2
#>   time           residual
#>   <date>            <dbl>
#> 1 1980-07-01 -0.000000883
#> 2 1980-10-01 -0.00000391 
#> 3 1981-01-01 -0.00000223 
#> 4 1981-04-01  0.00000123 
#> 5 1981-07-01 -0.00000161 
#> 6 1981-10-01  0.00000315 
```
