# Extract the Parameter Covariance Matrix of a Revision Model

Extract the Parameter Covariance Matrix of a Revision Model

## Usage

``` r
# S3 method for class 'revision_model'
vcov(object, ...)
```

## Arguments

- object:

  A fitted model object inheriting from
  [revision_model](https://docs.ropensci.org/reviser/reference/revision_model.md),
  such as a `kk_model` or a `jvn_model`.

- ...:

  Ignored.

## Value

The estimated parameter covariance matrix.

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
[`states()`](https://docs.ropensci.org/reviser/reference/states.md),
[`summary.revision_model()`](https://docs.ropensci.org/reviser/reference/summary.revision_model.md)

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
vcov(fit)
#>                 F0          G0_0          G0_1            v0          eps0
#> F0    5.361759e-03 -1.035662e-06 -8.186818e-06 -8.711730e-05  3.819624e-07
#> G0_0 -1.035662e-06 -2.265219e-06  1.153701e-06  3.032068e-08  3.924083e-08
#> G0_1 -8.186818e-06  1.153701e-06  5.735712e-03 -1.619414e-06 -1.613451e-08
#> v0   -8.711730e-05  3.032068e-08 -1.619414e-06  2.918697e-02 -5.520300e-09
#> eps0  3.819624e-07  3.924083e-08 -1.613451e-08 -5.520300e-09  5.058073e-07
```
