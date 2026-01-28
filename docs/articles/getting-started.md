# Getting Started with manureshed

``` r
library(manureshed)
#> 
#> =================================================================
#> manureshed package loaded successfully!
#> =================================================================
#> 
#> Built-in Data (Downloaded on-demand from OSF):
#>   • NuGIS data: 1987 - 2016 (all spatial scales)
#>   • WWTP data: 2007 - 2016 (nitrogen and phosphorus)
#>   • Spatial boundaries: county, HUC8, HUC2
#>   • Texas supplemental data (automatic for HUC8)
#> 
#> Quick Start:
#>   check_builtin_data()           # Check data availability
#>   download_all_data()            # Download all datasets
#>   quick_analysis()               # Complete analysis + visuals
#>   ?run_builtin_analysis          # Main workflow function
#> 
#> Data Management:
#>   clear_data_cache()             # Clear downloaded data
#>   download_osf_data()            # Download specific dataset
#> 
#> Documentation:
#>   vignette('getting-started')    # Getting started guide
#>   ?manureshed                    # Package overview
#> =================================================================
#> 
#> Data Summary:
#>   OSF Repository: https://osf.io/g39xa/
#>   Available scales: county, huc8, huc2
#>   Years available: 1987 - 2016
#>   WWTP years: 2007 - 2016 (nitrogen, phosphorus)
#>   Methodology Paper: Akanbi, O.D., Gupta, A., Mandayam, V., Flynn, K.C.,
#>       Yarus, J.M., Barcelos, E.I., French, R.H., 2026. Towards circular nutrient economies: An
#>       integrated manureshed framework for agricultural and municipal resource management.
#>       Resources, Conservation and Recycling, https://doi.org/10.1016/j.resconrec.2025.108697
#> 
#>   Cached datasets: 12/10 downloaded
#> 
```

## What is manureshed?

The `manureshed` package analyzes agricultural nutrient balances at
different spatial scales (county, HUC8 watershed, HUC2 region) and can
integrate wastewater treatment plant (WWTP) effluent data to show how
municipal nutrient loads affect agricultural areas.

## View cheatsheet

``` r
view_cheatsheet()
```

## Quick Start - Complete Analysis

The easiest way to get started is with
[`quick_analysis()`](https://exelegch.github.io/manureshed-docs/reference/quick_analysis.md):

``` r
# Complete analysis with maps and plots
results <- quick_analysis(
  scale = "huc8",           # Choose: "county", "huc8", or "huc2"
  year = 2016,              # Any year 1987-2016
  nutrients = "nitrogen",   # Choose: "nitrogen", "phosphorus", or both
  include_wwtp = TRUE       # Include wastewater plants (2007-2016 only)
)
```

This creates: - Classification maps - WWTP facility maps  
- Network plots - Comparison charts - All saved to your output directory

## Step-by-Step Analysis

### 1. Check Available Data

``` r
# See what data is available
check_builtin_data()

# Download all data (optional, ~40MB)
download_all_data()
```

### 2. Basic Agricultural Analysis

``` r
# Analyze just agricultural data
results <- run_builtin_analysis(
  scale = "county",
  year = 2010,
  nutrients = "nitrogen",
  include_wwtp = FALSE    # No WWTP data
)

# Quick summary
summarize_results(results)
```

### 3. Add WWTP Data

``` r
# Analysis with wastewater plants (2007-2016 available)
results_wwtp <- run_builtin_analysis(
  scale = "huc8",
  year = 2016,
  nutrients = c("nitrogen", "phosphorus"),
  include_wwtp = TRUE
)

# See the difference WWTP makes
comparison <- compare_analyses(results, results_wwtp, "nitrogen")
print(comparison)
```

## Understanding the Results

### Classifications

Each spatial unit gets classified into:

- **Source**: Has excess nutrients to export
- **Sink Deficit**: Needs nutrient imports
- **Sink Fertilizer**: Has fertilizer surplus, could accept manure
- **Within Watershed/County**: Balanced
- **Excluded**: Too little cropland to analyze

### Accessing Results

``` r
# Agricultural data with classifications
agri_data <- results$agricultural

# WWTP facility data
wwtp_facilities <- results$wwtp$nitrogen$facility_data

# Combined results (agricultural + WWTP)
combined_data <- results$integrated$nitrogen

# Analysis settings
parameters <- results$parameters
```

## Creating Maps

### Classification Maps

``` r
# Basic nitrogen map
n_map <- map_agricultural_classification(
  data = results$agricultural,
  nutrient = "nitrogen", 
  classification_col = "N_class",
  title = "Nitrogen Classifications"
)

# Save the map
save_plot(n_map, "nitrogen_map.png", width = 10, height = 8)
```

### WWTP Maps

``` r
# Map WWTP facilities
facility_map <- map_wwtp_points(
  results$wwtp$nitrogen$spatial_data,
  nutrient = "nitrogen",
  title = "Nitrogen WWTP Facilities"
)

# Map WWTP influence on agricultural areas
influence_map <- map_wwtp_influence(
  results$integrated$nitrogen,
  nutrient = "nitrogen", 
  title = "WWTP Influence on Nitrogen"
)
```

## Working with Different Years

### Single Years

``` r
# Any year 1987-2016 for agricultural data
results_1990 <- run_builtin_analysis(scale = "county", year = 1990, 
                                     nutrients = "nitrogen", include_wwtp = FALSE)

results_2005 <- run_builtin_analysis(scale = "huc8", year = 2005, 
                                     nutrients = "phosphorus", include_wwtp = FALSE)

# WWTP data available 2007-2016
results_2012 <- run_builtin_analysis(scale = "huc8", year = 2012, 
                                     nutrients = "nitrogen", include_wwtp = TRUE)
```

### Multiple Years

``` r
# Analyze several years at once
batch_results <- batch_analysis_years(
  years = 2014:2016,
  scale = "county", 
  nutrients = "nitrogen",
  include_wwtp = TRUE
)
```

## Using Custom WWTP Data

For years outside 2007-2016, provide your own WWTP data:

``` r
# Use your own WWTP files
results_2020 <- run_builtin_analysis(
  scale = "huc8",
  year = 2020,  # Agricultural data available
  nutrients = "nitrogen",
  include_wwtp = TRUE,
  custom_wwtp_nitrogen = "my_wwtp_data_2020.csv",
  wwtp_load_units = "lbs"  # Handle different units
)
```

## State-Specific Analysis

``` r
# Analyze a specific state
texas_results <- run_state_analysis(
  state = "TX",
  scale = "county",
  year = 2016,
  nutrients = "nitrogen",
  include_wwtp = TRUE
)

# Quick state analysis with maps
ohio_quick <- quick_state_analysis(
  state = "OH",
  scale = "huc8", 
  year = 2015,
  nutrients = "phosphorus"
)
```

## Loading Individual Datasets

``` r
# Load specific datasets
county_2016 <- load_builtin_nugis("county", 2016)
huc8_boundaries <- load_builtin_boundaries("huc8")
wwtp_nitrogen <- load_builtin_wwtp("nitrogen", 2012)

# Check what years are available
list_available_years()
```

## Tips for Success

### Memory Management

``` r
# For large analyses, clear cache if needed
clear_data_cache()

# Check package health
health_check()
```

### Quality Checks

``` r
# Always validate your results
quick_check(results)

# Get package citation
citation_info()
```

## Next Steps

- **Advanced Features**: See
  [`vignette("advanced-features")`](https://exelegch.github.io/manureshed-docs/articles/advanced-features.md)
  for state analysis, custom thresholds, parallel processing
- **Visualization Guide**: See
  [`vignette("visualization-guide")`](https://exelegch.github.io/manureshed-docs/articles/visualization-guide.md)
  for detailed mapping options  
- **Data Integration**: See
  [`vignette("data-integration")`](https://exelegch.github.io/manureshed-docs/articles/data-integration.md)
  for using custom datasets

## Getting Help

``` r
# Function documentation
?run_builtin_analysis
?quick_analysis
?map_agricultural_classification

# Package overview
?manureshed

# Check if everything is working
health_check()
```

That’s it! You now know the basics of using `manureshed` for nutrient
flow analysis.
