# Fitted Revision Models

`reviser` represents every fitted revision-nowcasting model as an S3
object that inherits from the common parent class `revision_model`. The
two concrete classes are
[`kk_nowcast()`](https://docs.ropensci.org/reviser/reference/kk_nowcast.md),
which returns a `kk_model`, and
[`jvn_nowcast()`](https://docs.ropensci.org/reviser/reference/jvn_nowcast.md),
which returns a `jvn_model`; both carry
`c("<family>_model", "revision_model", "list")` as their class
attribute.

The parent class holds everything the two families share. The standard
extractor generics [`coef()`](https://rdrr.io/r/stats/coef.html),
[`vcov()`](https://rdrr.io/r/stats/vcov.html),
[`logLik()`](https://rdrr.io/r/stats/logLik.html),
[`nobs()`](https://rdrr.io/r/stats/nobs.html),
[`fitted()`](https://rdrr.io/r/stats/fitted.values.html),
[`residuals()`](https://rdrr.io/r/stats/residuals.html),
[`predict()`](https://rdrr.io/r/stats/predict.html) and the `reviser`
generic
[`states()`](https://docs.ropensci.org/reviser/reference/states.md),
together with [`print()`](https://rdrr.io/r/base/print.html),
[`summary()`](https://rdrr.io/r/base/summary.html) and
[`plot()`](https://rdrr.io/r/graphics/plot.default.html), are defined
once for `revision_model` and inherited by both families. Only the
handful of behaviors that genuinely differ between the families are
dispatched separately, through the internal generics `model_family()`,
`spec_lines()`, `signal_state()`, `target_column()` and
`default_plot_state()`.

A fitted object is a list with at least the components `params` (a data
frame with columns `Parameter`, `Estimate` and `Std.Error`), `states` (a
long tibble of state estimates, or `NULL` when the model was fitted with
`return_states = FALSE`), `loglik`, `n_param`, `n_ic`, `cov` and `data`.
A new model family becomes a full citizen of this system by returning an
object with those components, prepending `"revision_model"` to its class
attribute, and supplying methods for the five internal generics above.

## Value

This topic documents a class rather than a function.
[`kk_nowcast()`](https://docs.ropensci.org/reviser/reference/kk_nowcast.md)
returns a list of the components described above with class attribute
`c("kk_model", "revision_model", "list")`, and
[`jvn_nowcast()`](https://docs.ropensci.org/reviser/reference/jvn_nowcast.md)
returns the same with `"jvn_model"` in place of `"kk_model"`.

## See also

[`kk_nowcast()`](https://docs.ropensci.org/reviser/reference/kk_nowcast.md),
[`jvn_nowcast()`](https://docs.ropensci.org/reviser/reference/jvn_nowcast.md),
[`states()`](https://docs.ropensci.org/reviser/reference/states.md)

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
fit <- kk_nowcast(df, e = 1, model = "KK", method = "OLS")

# The fitted object carries the shared parent class.
class(fit)
#> [1] "kk_model"       "revision_model" "list"          
inherits(fit, "revision_model")
#> [1] TRUE

# The extractor generics are inherited from that parent.
head(coef(fit))
#>           F0         G0_0         G0_1           v0         eps0 
#>  0.200854859  0.995563965 -0.001695210  1.598322193  0.006626059 
head(states(fit))
#> # A tibble: 6 × 7
#>   time       state           estimate  lower  upper filter   sample   
#>   <date>     <chr>              <dbl>  <dbl>  <dbl> <chr>    <chr>    
#> 1 1980-07-01 release_1_lag_0   -0.154 -0.157 -0.152 smoothed in_sample
#> 2 1980-10-01 release_1_lag_0    1.78   1.78   1.78  smoothed in_sample
#> 3 1981-01-01 release_1_lag_0    1.94   1.94   1.95  smoothed in_sample
#> 4 1981-04-01 release_1_lag_0   -0.699 -0.702 -0.697 smoothed in_sample
#> 5 1981-07-01 release_1_lag_0    1.19   1.19   1.19  smoothed in_sample
#> 6 1981-10-01 release_1_lag_0   -1.18  -1.18  -1.18  smoothed in_sample
```
