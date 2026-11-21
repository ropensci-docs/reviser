# Fitted Latent Values from a Revision Model

Returns the smoothed estimate of the model's latent signal for the
in-sample periods, i.e. the revision-adjusted series. The signal is the
latent efficient value for a `kk_model` and the latent true value for a
`jvn_model`.

## Usage

``` r
# S3 method for class 'revision_model'
fitted(object, ...)
```

## Arguments

- object:

  A fitted model object inheriting from
  [revision_model](https://docs.ropensci.org/reviser/reference/revision_model.md),
  such as a `kk_model` or a `jvn_model`.

- ...:

  Ignored.

## Value

A tibble with columns `time`, `estimate`, `lower` and `upper`.

## See also

Other revision nowcasting:
[`coef.revision_model()`](https://docs.ropensci.org/reviser/reference/coef.revision_model.md),
[`jvn_nowcast()`](https://docs.ropensci.org/reviser/reference/jvn_nowcast.md),
[`kk_nowcast()`](https://docs.ropensci.org/reviser/reference/kk_nowcast.md),
[`logLik.revision_model()`](https://docs.ropensci.org/reviser/reference/logLik.revision_model.md),
[`nobs.revision_model()`](https://docs.ropensci.org/reviser/reference/nobs.revision_model.md),
[`plot.revision_model()`](https://docs.ropensci.org/reviser/reference/plot.revision_model.md),
[`predict.revision_model()`](https://docs.ropensci.org/reviser/reference/predict.revision_model.md),
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
fit <- kk_nowcast(df, e = 1, model = "KK", method = "MLE")
head(fitted(fit))
#> # A tibble: 6 × 4
#>   time       estimate  lower  upper
#>   <date>        <dbl>  <dbl>  <dbl>
#> 1 1980-07-01   -0.154 -0.157 -0.152
#> 2 1980-10-01    1.78   1.78   1.78 
#> 3 1981-01-01    1.94   1.94   1.95 
#> 4 1981-04-01   -0.699 -0.702 -0.697
#> 5 1981-07-01    1.19   1.19   1.19 
#> 6 1981-10-01   -1.18  -1.18  -1.18 
```
