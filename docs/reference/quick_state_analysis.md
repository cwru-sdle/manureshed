# Quick State Analysis with Visualization

Run state-level analysis with automatic visualizations

## Usage

``` r
quick_state_analysis(
  state,
  scale = "huc8",
  year = 2016,
  nutrients = c("nitrogen", "phosphorus"),
  include_wwtp = TRUE,
  output_dir = file.path(tempdir(), paste0("state_", tolower(state), "_results")),
  create_maps = TRUE,
  create_networks = TRUE,
  create_comparisons = TRUE,
  verbose = TRUE,
  ...
)
```

## Arguments

- state:

  Character. Two-letter state abbreviation

- scale:

  Character. Spatial scale

- year:

  Numeric. Year to analyze

- nutrients:

  Character vector. Nutrients to analyze

- include_wwtp:

  Logical. Include WWTP analysis

- output_dir:

  Character. Output directory

- create_maps:

  Logical. Create maps

- create_networks:

  Logical. Create network plots

- create_comparisons:

  Logical. Create comparison plots

- verbose:

  Logical. Show progress

- ...:

  Additional arguments

## Value

List with results and visualizations

## Examples

``` r
# \donttest{
# Quick state analysis - use states with good data coverage
results <- quick_state_analysis(
  state = "TX",  # Texas has good data coverage
  scale = "county",
  year = 2016,
  nutrients = "nitrogen",
  include_wwtp = TRUE
)
#> 
#> ======================================================================
#> STATE-LEVEL MANURESHED ANALYSIS
#> ======================================================================
#> State:TX
#> Scale:county
#> Year:2016
#> ----------------------------------------------------------------------
#> Loading national data...
#> Filtering to stateTX...
#> Filtered to state TX: 248 spatial units
#> Filtered to state TX: 254 spatial units
#> Processing agricultural classifications...
#> Starting complete agricultural classification for county scale...
#> Processed NuGIS data for county scale:
#>   Spatial units: 248
#>   Converted P2O5 to P using factor: 0.436
#> Nitrogen classification summary:
#>   Excluded: 9 units
#>   Sink_Deficit: 199 units
#>   Sink_Fertilizer: 22 units
#>   Source: 5 units
#>   Within_County: 13 units
#> Phosphorus classification summary:
#>   Excluded: 9 units
#>   Sink_Deficit: 126 units
#>   Sink_Fertilizer: 28 units
#>   Source: 35 units
#>   Within_County: 50 units
#> Agricultural classification complete!
#> Applied threshold: 1235.53 acres
#> Processing state WWTP data...
#> Filtered for positive nitrogen loads:
#>   Original: 1397 facilities
#>   With positive loads: 1397 facilities
#> WWTP nitrogen source classification:
#>   Minor Source: 1323 facilities
#>   Small Source: 52 facilities
#>   Medium Source: 15 facilities
#>   Large Source: 7 facilities
#>   Very Large Source: 0 facilities
#> Created spatial WWTP data with 1397 facilities
#> Looking for boundary ID column: 'FIPS'
#> Available columns in boundaries: FIPS, County, State_Name, geometry
#> Aggregating WWTP nitrogen loads by spatial boundaries...
#> Aggregation complete:
#>   WWTP facilities: 1397
#>   Spatial units with facilities: 176
#>   Total nitrogen load: 6377.22 tons/year
#> Integrating WWTP and agricultural data...
#> Integrating WWTP nitrogen data with agricultural classifications...
#> Using agricultural ID column: FIPS
#> Combined nitrogen classification summary:
#>   Excluded: 9 units
#>   Sink_Deficit: 197 units
#>   Sink_Fertilizer: 21 units
#>   Source: 8 units
#>   Within_County: 19 units
#> 
#> ======================================================================
#> STATE ANALYSIS COMPLETE
#> ======================================================================
#> State:TX
#> Spatial units:254
#> WWTP facilities:1397
#> ======================================================================
#> 
#> Generating state visualizations...
#> Retrieving data for the year 2024
#> Saved plot to: /tmp/Rtmp0dSqZ3/state_tx_results/map_tx_agricultural_nitrogen_2016.png
#> Dimensions: 10 x 8 in at 300 DPI
#> File size: 436.41 KB
#> Device: png
#> Retrieving data for the year 2024
#> Saved plot to: /tmp/Rtmp0dSqZ3/state_tx_results/map_tx_combined_nitrogen_2016.png
#> Dimensions: 10 x 8 in at 300 DPI
#> File size: 435.83 KB
#> Device: png
# }
```
