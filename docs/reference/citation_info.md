# Display Package Citation Information

Provides citation information for the package and data sources. Prints
formatted citation text to the console for the manureshed package, the
underlying research methodology paper (Akanbi et al., 2026), and the
primary data sources (NuGIS agricultural data and EPA WWTP discharge
data). The function is designed for users to easily obtain proper
citations for publications and reports.

## Usage

``` r
citation_info()
```

## Value

No return value, called for side effects. The function prints citation
information to the console including:

- Package citation with version and OSF repository

- Research methodology paper citation

- NuGIS data source attribution

- EPA WWTP data source attribution

- Contact information for data sources

## Details

This function takes no arguments. It prints citation information
directly to the console using message() functions, which can be
suppressed with suppressMessages() if needed.

## Note

This function requires no arguments and can be called simply as
`citation_info()`.

## See also

[`check_builtin_data`](https://exelegch.github.io/manureshed-docs/reference/check_builtin_data.md)
for data availability,
[`health_check`](https://exelegch.github.io/manureshed-docs/reference/health_check.md)
for package diagnostics

## Examples

``` r
# \donttest{
# Display citation information
citation_info()
#> To cite the manureshed package in publications, use:
#> Akanbi, O. D.; Mandayam, V.; Gupta, A.; Flynn, K. C.; Yarus, J. M.;
#> Barcelos, E. I.; & French, R. H. (2025).
#> manureshed: An Open-Source R Package for Scalable Temporal and Multi-Regional
#> Analysis of Integrated Agricultural-Municipal Nutrient Flows.
#> R package version 0.1.2.
#> OSF Repository: https://osf.io/g39xa/
#> For the underlying research methodology, cite:
#> Akanbi, O. D.; Gupta, A.; Mandayam, V.; Flynn, K. C.; Yarus, J. M.;
#> Barcelos, E. I.; French, R. H. Towards Circular Nutrient Economies: An Integrated
#> Manureshed Framework for Agricultural and Municipal Resource Management.
#> Resources, Conservation and Recycling, 2025. https://doi.org/10.1016/j.resconrec.2025.108697
#> ======================================================================
#> DATA SOURCES
#> ======================================================================
#> NuGIS Agricultural Data (1987-2016):
#>   NuGIS (Nutrient Use Geographic Information System).
#>   The Fertilizer Institute (TFI) and Plant Nutrition Canada (PNC).
#>   Available at: https://nugis.tfi.org/tabular_data
#>   
#>   Note: The manureshed package uses cleaned and quality-controlled
#>   versions of NuGIS data, with resolved metadata issues and enhanced
#>   spatial integration, as described in Akanbi et al. (2025).
#> EPA WWTP Discharge Data (2007-2016):
#>   U.S. Environmental Protection Agency (EPA).
#>   Discharge Monitoring Report (DMR) Loading Tool.
#>   Enforcement and Compliance History Online (ECHO).
#>   Available at: https://echo.epa.gov/trends/loading-tool/water-pollution-search
#> For questions about data usage and attribution, contact:
#>   NuGIS: nugis@tfi.org
#>   Package: olatunde.akanbi@case.edu
# }
```
