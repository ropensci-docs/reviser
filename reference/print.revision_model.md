# Print Method for Revision Models

Default print method for objects inheriting from
[revision_model](https://docs.ropensci.org/reviser/reference/revision_model.md).
Dispatches to
[`summary.revision_model()`](https://docs.ropensci.org/reviser/reference/summary.revision_model.md)
for a consistent console display.

## Usage

``` r
# S3 method for class 'revision_model'
print(x, ...)
```

## Arguments

- x:

  A fitted model object inheriting from
  [revision_model](https://docs.ropensci.org/reviser/reference/revision_model.md),
  such as a `kk_model` or a `jvn_model`.

- ...:

  Additional arguments passed to
  [`summary.revision_model()`](https://docs.ropensci.org/reviser/reference/summary.revision_model.md).

## Value

The input `x`, invisibly.

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
fit <- kk_nowcast(df, e = 1, h = 2, model = "Kishor-Koenig", method = "MLE")
fit
#> 
#> === Kishor-Koenig Model ===
#> 
#> Specification: Kishor-Koenig 
#> Estimation method: MLE 
#> Convergence: Success 
#> Log-likelihood: -100.83 
#> AIC: 211.67 
#> BIC: 230.99 
#> 
#> Parameter Estimates:
#>  Parameter Estimate Std.Error
#>         F0    0.198     0.073
#>       G0_0    0.990     0.000
#>       G0_1    0.080     0.076
#>         v0    1.598     0.171
#>       eps0    0.007     0.001
#> 
```
