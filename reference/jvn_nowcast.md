# Jacobs-Van Norden Model for Data Revisions

Estimate the Jacobs and Van Norden (2011) state-space model for
real-time data revisions, allowing for news and noise components and
optional spillovers.

## Usage

``` r
jvn_nowcast(
  df,
  e,
  ar_order = 1,
  h = 0,
  include_news = TRUE,
  include_noise = TRUE,
  include_spillovers = FALSE,
  spillover_news = TRUE,
  spillover_noise = TRUE,
  method = "MLE",
  alpha = 0.05,
  standardize = FALSE,
  solver_options = list()
)
```

## Arguments

- df:

  A matrix, data frame, or single-ID vintages object. Wide data should
  store one vintage per column. Long-format vintages data are also
  accepted and are converted internally. If `df` is a matrix, or a data
  frame without a `time` column, a synthetic `time` index is created.

- e:

  A single integer giving the number of vintages used in estimation. The
  function uses the first `e` vintage columns after `time`, so `e` must
  be greater than `0` and no larger than the number of available vintage
  columns.

- ar_order:

  A single integer giving the autoregressive order of the latent
  true-value process. Must be greater than `0`.

- h:

  A single integer giving the forecast horizon. Must be greater than or
  equal to `0`.

- include_news:

  Logical; whether to include a news component.

- include_noise:

  Logical; whether to include a noise component.

- include_spillovers:

  Logical; whether to include spillover effects.

- spillover_news:

  Logical; whether spillovers apply to the news component.

- spillover_noise:

  Logical; whether spillovers apply to the noise component.

- method:

  Estimation method. Currently only `"MLE"` is supported.

- alpha:

  Significance level used for confidence intervals. Must lie in
  `(0, 1)`.

- standardize:

  Logical; whether to standardize the vintage matrix before estimation
  using `jvn_standardize()`. If `TRUE`, scaling metadata are returned in
  the `scale` element of the output.

- solver_options:

  A named list of solver options. Valid names are `trace`, `method`,
  `maxiter`, `transform_se`, `startvals`, `se_method`, `n_starts`,
  `seed`, `return_states`, `qml_eps`, `qml_score_method`, `qml_scale`,
  `sigma_lower`, `sigma_upper`, `kfas_init`, and `ic_n`. Supported
  entries are:

  - `trace`: integer controlling console output.

  - `method`: optimization method; one of `"L-BFGS-B"`, `"BFGS"`,
    `"Nelder-Mead"`, `"nlminb"`, or `"two-step"`.

  - `maxiter`: maximum number of optimizer iterations.

  - `transform_se`: logical; whether standard deviation parameters are
    optimized on the log scale.

  - `startvals`: optional numeric vector of starting values. The vector
    must have length equal to the number of estimated parameters and
    must follow the internal parameter order used by
    `jvn_param_table()`: AR coefficients `rho_*`, `sigma_e`, optional
    `sigma_nu_*`, optional `sigma_zeta_*`, and optional spillover
    parameters `T_nu_*` and `T_zeta_*`.

  - `se_method`: standard-error method; one of `"hessian"`, `"qml"`, or
    `"none"`.

  - `n_starts`: number of random starting points for multi-start
    optimization.

  - `seed`: optional random seed used for multi-start perturbations.

  - `return_states`: logical; whether filtered and smoothed state
    estimates should be returned.

  - `qml_eps`: finite-difference step size used in QML covariance
    estimation.

  - `qml_score_method`: score approximation method; `"forward"` or
    `"central"`.

  - `qml_scale`: scaling convention for the QML covariance; `"sum"`,
    `"mean"`, or `"hc"`.

  - `sigma_lower`: lower bound for standard deviations on the natural
    scale.

  - `sigma_upper`: upper bound for standard deviations on the natural
    scale.

  - `kfas_init`: initialization used in the KFAS filtering/smoothing
    stage; `"stationary"` or `"diffuse"`. This affects state extraction,
    not the custom likelihood engine.

  - `ic_n`: sample-size convention used for BIC; `"T"` for the paper
    convention or `"Tp"` for `T * n_vint`.

  For backward compatibility, the legacy aliases `score_method` and
  `score_eps` are also accepted and mapped to `qml_score_method` and
  `qml_eps`.

## Value

An object of class `"jvn_model"` with components:

- states:

  A tibble of filtered and smoothed state estimates. If
  `solver_options$return_states = FALSE`, this is `NULL`.

- jvn_model_mat:

  A list containing the state-space matrices `Z`, `Tmat`, `R`, `H`, and
  `Q`.

- params:

  A data frame of parameter estimates and standard errors.

- fit:

  The raw optimizer output returned by the selected numerical optimizer.

- loglik:

  The maximized log-likelihood.

- aic:

  Akaike information criterion.

- bic:

  Bayesian information criterion.

- convergence:

  Optimizer convergence code.

- data:

  The input data after preprocessing.

- scale:

  Scaling metadata returned by `jvn_standardize()` when
  `standardize = TRUE`; otherwise `NULL`.

- se_method:

  The standard-error method used.

- cov:

  Estimated covariance matrix of the parameter estimates, if available;
  otherwise `NULL`.

- p0_regularized:

  Logical; whether computing the Kalman filter's stationary
  initial-state covariance at the converged estimate required numerical
  regularization, which can happen for a fit close to a non-stationary
  boundary. `NULL` when `solver_options$return_states = FALSE`, since
  the initial-state covariance is then not computed.
  [`summary()`](https://rdrr.io/r/base/summary.html) reports this when
  `TRUE`.

## References

Jacobs, Jan P. A. M. and Van Norden, Simon (2011). Modeling data
revisions: Measurement error and dynamics of "true" values. *Journal of
Econometrics*.

## See also

Other revision nowcasting:
[`coef.revision_model()`](https://docs.ropensci.org/reviser/reference/coef.revision_model.md),
[`fitted.revision_model()`](https://docs.ropensci.org/reviser/reference/fitted.revision_model.md),
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
# \donttest{
gdp_growth <- dplyr::filter(
  tsbox::ts_pc(reviser::gdp),
  id == "EA",
  time >= min(pub_date),
  time <= as.Date("2020-01-01")
)
gdp_growth <- tidyr::drop_na(gdp_growth)
df <- get_nth_release(gdp_growth, n = 0:3)

result <- jvn_nowcast(
  df = df,
  e = 4,
  ar_order = 2,
  h = 0,
  include_news = TRUE,
  include_noise = TRUE
)
summary(result)
#> 
#> === Jacobs-Van Norden Model ===
#> 
#> Specification: news and noise 
#> AR order: 2 
#> Components: news = TRUE | noise = TRUE | spillovers = FALSE 
#> Estimation method: MLE 
#> Convergence: Success 
#> Log-likelihood: 256.22 
#> AIC: -490.44 
#> BIC: -465.7 
#> 
#> Parameter Estimates:
#>     Parameter Estimate Std.Error
#>         rho_1    0.900     0.278
#>         rho_2   -0.236     0.234
#>       sigma_e    0.001     0.573
#>    sigma_nu_1    0.070     0.006
#>    sigma_nu_2    0.052     0.004
#>    sigma_nu_3    0.001     0.036
#>    sigma_nu_4    0.633     0.210
#>  sigma_zeta_1    0.001     0.021
#>  sigma_zeta_2    0.001     0.009
#>  sigma_zeta_3    0.001     0.017
#>  sigma_zeta_4    0.042     0.004
#> 
# }
```
