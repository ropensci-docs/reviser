# Plot Revision Model Results

Plot filtered or smoothed estimates for a selected state from a fitted
revision model. Defined once for the parent class
[revision_model](https://docs.ropensci.org/reviser/reference/revision_model.md)
and inherited by `kk_model` and `jvn_model` objects alike; the state
shown when `state` is not given is chosen by the concrete class.

## Usage

``` r
# S3 method for class 'revision_model'
plot(x, state = NULL, type = "filtered", ...)
```

## Arguments

- x:

  A fitted model object inheriting from
  [revision_model](https://docs.ropensci.org/reviser/reference/revision_model.md),
  such as a `kk_model` or a `jvn_model`.

- state:

  String. The name of the state to visualize. If `NULL`, the family's
  default state is used: the latent true value for a `jvn_model`, and
  the first available state for a `kk_model`.

- type:

  String. Type of estimate: "filtered" or "smoothed".

- ...:

  Additional arguments passed to theme_reviser.

## Value

A `ggplot2` object.

## Details

This method requires the state estimates to be available. A model fitted
with `solver_options$return_states = FALSE` did not retain them, and
plotting it fails with a message naming that option, in the same way
[`states()`](https://docs.ropensci.org/reviser/reference/states.md),
[`fitted()`](https://rdrr.io/r/stats/fitted.values.html),
[`residuals()`](https://rdrr.io/r/stats/residuals.html) and
[`predict()`](https://rdrr.io/r/stats/predict.html) do.

## See also

Other revision nowcasting:
[`coef.revision_model()`](https://docs.ropensci.org/reviser/reference/coef.revision_model.md),
[`fitted.revision_model()`](https://docs.ropensci.org/reviser/reference/fitted.revision_model.md),
[`jvn_nowcast()`](https://docs.ropensci.org/reviser/reference/jvn_nowcast.md),
[`kk_nowcast()`](https://docs.ropensci.org/reviser/reference/kk_nowcast.md),
[`logLik.revision_model()`](https://docs.ropensci.org/reviser/reference/logLik.revision_model.md),
[`nobs.revision_model()`](https://docs.ropensci.org/reviser/reference/nobs.revision_model.md),
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
    tsbox::ts_pc(
      dplyr::filter(reviser::gdp, id == "US")
    ),
    start = "1980-01-01"
  ),
  n = 0:1
)
df <- dplyr::select(df, -c("id", "pub_date"))
df <- na.omit(df)

e <- 1 # Number of efficient release
h <- 2 # Forecast horizon
result <- kk_nowcast(df, e, h = h, model = "Kishor-Koenig")

plot(result)

```
