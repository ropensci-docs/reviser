# Package index

### Revision analysis

Functions for analyzing revisions of time series.

- [`diagnose()`](https://docs.ropensci.org/reviser/reference/diagnose.md)
  : Diagnose Revision Quality
- [`diagnose(`*`<revision_summary>`*`)`](https://docs.ropensci.org/reviser/reference/diagnose.revision_summary.md)
  : Diagnose Method for Revision Summary
- [`get_first_efficient_release()`](https://docs.ropensci.org/reviser/reference/get_first_efficient_release.md)
  : Identify the First Efficient Release in Vintage Data
- [`get_revision_analysis()`](https://docs.ropensci.org/reviser/reference/get_revision_analysis.md)
  : Revision Analysis Summary Statistics
- [`print(`*`<lst_efficient>`*`)`](https://docs.ropensci.org/reviser/reference/print.lst_efficient.md)
  : Print Method for Efficient Release Results
- [`print(`*`<revision_summary>`*`)`](https://docs.ropensci.org/reviser/reference/print.revision_summary.md)
  : Print Method for Revision Summary
- [`summary(`*`<lst_efficient>`*`)`](https://docs.ropensci.org/reviser/reference/summary.lst_efficient.md)
  : Summary of Efficient Release Models
- [`summary(`*`<revision_summary>`*`)`](https://docs.ropensci.org/reviser/reference/summary.revision_summary.md)
  : Summary Method for Revision Summary

### Revision utilities

Utility functions for working with revisions of time series.

- [`get_days_to_release()`](https://docs.ropensci.org/reviser/reference/get_days_to_release.md)
  : Calculate the Number of Days Between Period End and First Release
- [`get_first_release()`](https://docs.ropensci.org/reviser/reference/get_first_release.md)
  : Extract the First Data Release (Vintage)
- [`get_fixed_release()`](https://docs.ropensci.org/reviser/reference/get_fixed_release.md)
  : Extract Vintage Values from a Data Frame
- [`get_latest_release()`](https://docs.ropensci.org/reviser/reference/get_latest_release.md)
  : Extract the Latest Data Release (Vintage)
- [`get_nth_release()`](https://docs.ropensci.org/reviser/reference/get_nth_release.md)
  : Extract the Nth Data Release (Vintage)
- [`get_releases_by_date()`](https://docs.ropensci.org/reviser/reference/get_releases_by_date.md)
  : Get Data Releases for a Specific Date
- [`get_revisions()`](https://docs.ropensci.org/reviser/reference/get_revisions.md)
  : Calculate Revisions in Vintage Data

### Revision nowcasting

Functions for nowcasting revisions of time series.

- [`coef(`*`<revision_model>`*`)`](https://docs.ropensci.org/reviser/reference/coef.revision_model.md)
  : Extract Parameter Estimates from a Revision Model
- [`fitted(`*`<revision_model>`*`)`](https://docs.ropensci.org/reviser/reference/fitted.revision_model.md)
  : Fitted Latent Values from a Revision Model
- [`jvn_nowcast()`](https://docs.ropensci.org/reviser/reference/jvn_nowcast.md)
  : Jacobs-Van Norden Model for Data Revisions
- [`kk_nowcast()`](https://docs.ropensci.org/reviser/reference/kk_nowcast.md)
  : Generalized Kishor-Koenig Model for Nowcasting
- [`logLik(`*`<revision_model>`*`)`](https://docs.ropensci.org/reviser/reference/logLik.revision_model.md)
  : Extract the Log-Likelihood of a Revision Model
- [`nobs(`*`<revision_model>`*`)`](https://docs.ropensci.org/reviser/reference/nobs.revision_model.md)
  : Number of Observations Used to Fit a Revision Model
- [`plot(`*`<revision_model>`*`)`](https://docs.ropensci.org/reviser/reference/plot.revision_model.md)
  : Plot Revision Model Results
- [`predict(`*`<revision_model>`*`)`](https://docs.ropensci.org/reviser/reference/predict.revision_model.md)
  : Forecasts from a Revision Model
- [`print(`*`<revision_model>`*`)`](https://docs.ropensci.org/reviser/reference/print.revision_model.md)
  : Print Method for Revision Models
- [`residuals(`*`<revision_model>`*`)`](https://docs.ropensci.org/reviser/reference/residuals.revision_model.md)
  : Residuals of a Revision Model
- [`revision_model`](https://docs.ropensci.org/reviser/reference/revision_model.md)
  : Fitted Revision Models
- [`states()`](https://docs.ropensci.org/reviser/reference/states.md) :
  Extract the Latent State Estimates of a Revision Model
- [`summary(`*`<revision_model>`*`)`](https://docs.ropensci.org/reviser/reference/summary.revision_model.md)
  : Summary Method for Revision Models
- [`vcov(`*`<revision_model>`*`)`](https://docs.ropensci.org/reviser/reference/vcov.revision_model.md)
  : Extract the Parameter Covariance Matrix of a Revision Model

### Revision graphs

Functions for plotting revisions of time series.

- [`plot(`*`<tbl_vintage>`*`)`](https://docs.ropensci.org/reviser/reference/plot.tbl_vintage.md)
  : Plot Method for Vintages Data
- [`plot_vintages()`](https://docs.ropensci.org/reviser/reference/plot_vintages.md)
  : Plot Vintages Data
- [`theme_reviser()`](https://docs.ropensci.org/reviser/reference/theme_reviser.md)
  [`colors_reviser()`](https://docs.ropensci.org/reviser/reference/theme_reviser.md)
  [`scale_color_reviser()`](https://docs.ropensci.org/reviser/reference/theme_reviser.md)
  [`scale_fill_reviser()`](https://docs.ropensci.org/reviser/reference/theme_reviser.md)
  : Custom Visualization Theme and Color Scales for reviser

### Helpers

Helper functions to convert revisions to a tidy format.

- [`print(`*`<tbl_vintage>`*`)`](https://docs.ropensci.org/reviser/reference/print.tbl_vintage.md)
  : Print Method for Vintages Data
- [`summary(`*`<tbl_vintage>`*`)`](https://docs.ropensci.org/reviser/reference/summary.tbl_vintage.md)
  : Summary Method for Vintages Data
- [`tbl_sum(`*`<tbl_vintage>`*`)`](https://docs.ropensci.org/reviser/reference/tbl_sum.tbl_vintage.md)
  : Tibble Summary for Vintages Data
- [`tbl_vintage`](https://docs.ropensci.org/reviser/reference/tbl_vintage.md)
  : Vintages Data Objects
- [`validate_vintages()`](https://docs.ropensci.org/reviser/reference/validate_vintages.md)
  : Vintages Data Classes and Their Validation
- [`vintages_long()`](https://docs.ropensci.org/reviser/reference/vintages_long.md)
  : Convert Vintages Data to Long Format
- [`vintages_wide()`](https://docs.ropensci.org/reviser/reference/vintages_wide.md)
  : Convert Vintages Data to Wide Format

### Data

GDP data used in the package.

- [`gdp`](https://docs.ropensci.org/reviser/reference/gdp.md) : Vintages
  Data

### Package overview

Package-level documentation.
