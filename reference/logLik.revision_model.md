# Extract the Log-Likelihood of a Revision Model

The returned object carries the degrees of freedom and effective number
of observations used by the model, so
[`stats::AIC()`](https://rdrr.io/r/stats/AIC.html) and
[`stats::BIC()`](https://rdrr.io/r/stats/AIC.html) reproduce the values
reported by [`summary()`](https://rdrr.io/r/base/summary.html).

## Usage

``` r
# S3 method for class 'revision_model'
logLik(object, ...)
```

## Arguments

- object:

  A fitted model object inheriting from
  [revision_model](https://docs.ropensci.org/reviser/reference/revision_model.md),
  such as a `kk_model` or a `jvn_model`.

- ...:

  Ignored.

## Value

An object of class `logLik`.

## See also

Other revision nowcasting:
[`coef.revision_model()`](https://docs.ropensci.org/reviser/reference/coef.revision_model.md),
[`fitted.revision_model()`](https://docs.ropensci.org/reviser/reference/fitted.revision_model.md),
[`jvn_nowcast()`](https://docs.ropensci.org/reviser/reference/jvn_nowcast.md),
[`kk_nowcast()`](https://docs.ropensci.org/reviser/reference/kk_nowcast.md),
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
logLik(fit)
#> 'log Lik.' -100.8349 (df=5)
AIC(fit)
#> [1] 211.6698
BIC(fit)
#> [1] 230.988
```
