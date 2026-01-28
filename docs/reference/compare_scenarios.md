# Compare Multiple Analysis Scenarios

Compare results from multiple analysis runs side-by-side with
visualizations and summary statistics.

## Usage

``` r
compare_scenarios(
  scenario_list,
  metrics = c("sources", "sinks", "balanced", "excluded"),
  create_plots = TRUE,
  output_dir = NULL
)
```

## Arguments

- scenario_list:

  Named list of analysis results from run_builtin_analysis()

- metrics:

  Character vector of metrics to compare. Options: "sources", "sinks",
  "balanced", "excluded", "total_surplus", "total_deficit"

- create_plots:

  Logical. Create comparison plots? (default: TRUE)

- output_dir:

  Character. Directory for saving plots (default: NULL, no save)

## Value

List containing:

- comparison_data:

  Data frame with metrics for each scenario

- plots:

  List of ggplot objects (if create_plots = TRUE)

- summary:

  Summary statistics

## Examples

``` r
# \donttest{
# Create multiple scenarios
base <- run_builtin_analysis(year = 2016, include_wwtp = FALSE,
                              scale = "county", nutrients = "nitrogen")
#> 
#> ======================================================================
#> BATCH MANURESHED ANALYSIS
#> ======================================================================
#> Year: 2016
#> Scale: county
#> Nutrients: nitrogen
#> ----------------------------------------------------------------------
#> Checking data availability...
#> Data availability confirmed
#>   Available scales:county, huc8, huc2
#>   Available years forcounty:1987-2016
#>   Built-in WWTP data:Available (2007-2016)
#> 
#> Loading built-in NuGIS data...
#> Using cached version of nugis_county_data
#> Loaded NuGIS county data for year 2016
#> Number of spatial units: 3058
#> Loading built-in spatial boundaries...
#> Using cached version of county_boundaries
#> Loaded county boundaries
#> Number of spatial units: 3112
#> Calculating cropland threshold...
#> Cropland threshold:1235.53acres
#> 
#> Processing agricultural classifications...
#> Starting complete agricultural classification for county scale...
#> Processed NuGIS data for county scale:
#>   Spatial units: 3058
#>   Converted P2O5 to P using factor: 0.436
#> Nitrogen classification summary:
#>   Excluded: 158 units
#>   Sink_Deficit: 2450 units
#>   Sink_Fertilizer: 214 units
#>   Source: 83 units
#>   Within_County: 153 units
#> Phosphorus classification summary:
#>   Excluded: 158 units
#>   Sink_Deficit: 1891 units
#>   Sink_Fertilizer: 372 units
#>   Source: 317 units
#>   Within_County: 320 units
#> Agricultural classification complete!
#> Applied threshold: 1235.53 acres
#> Agricultural classification complete
#>   Spatial units processed:3112
#>   Nitrogen classes:Excluded ( 212 ), Sink_Deficit ( 2450 ), Sink_Fertilizer ( 214 ), Source ( 83 ), Within_County ( 153 )
#>   Phosphorus classes:Excluded ( 212 ), Sink_Deficit ( 1891 ), Sink_Fertilizer ( 372 ), Source ( 317 ), Within_County ( 320 )
#> 
#> WWTP analysis skipped
#> 
#> Saving results...
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/county_agricultural_2016.rds
#> File size: 1.04 MB
#> Rows: 3112, Columns: 17
#> Geometry type: POLYGON
#> CRS: EPSG:5070
#> Saved analysis summary to: /tmp/Rtmp0dSqZ3/analysis_summary_2016.rds
#> Format: RDS
#> File size: 0.49 KB
#>  Results saved to:/tmp/Rtmp0dSqZ3
#>   Files created:2
#> 
#> ======================================================================
#> ANALYSIS COMPLETE
#> ======================================================================
#> Processing time:0.01minutes
#> Scale:county
#> Year:2016
#> Nutrients analyzed:nitrogen
#> Spatial units:3112
#> Output directory:/tmp/Rtmp0dSqZ3
#> ======================================================================
wwtp <- run_builtin_analysis(year = 2016, include_wwtp = TRUE,
                              scale = "county", nutrients = "nitrogen")
#> 
#> ======================================================================
#> BATCH MANURESHED ANALYSIS
#> ======================================================================
#> Year: 2016
#> Scale: county
#> Nutrients: nitrogen
#> ----------------------------------------------------------------------
#> Checking data availability...
#> Data availability confirmed
#>   Available scales:county, huc8, huc2
#>   Available years forcounty:1987-2016
#>   Built-in WWTP data:Available (2007-2016)
#> 
#> Loading built-in NuGIS data...
#> Using cached version of nugis_county_data
#> Loaded NuGIS county data for year 2016
#> Number of spatial units: 3058
#> Loading built-in spatial boundaries...
#> Using cached version of county_boundaries
#> Loaded county boundaries
#> Number of spatial units: 3112
#> Calculating cropland threshold...
#> Cropland threshold:1235.53acres
#> 
#> Processing agricultural classifications...
#> Starting complete agricultural classification for county scale...
#> Processed NuGIS data for county scale:
#>   Spatial units: 3058
#>   Converted P2O5 to P using factor: 0.436
#> Nitrogen classification summary:
#>   Excluded: 158 units
#>   Sink_Deficit: 2450 units
#>   Sink_Fertilizer: 214 units
#>   Source: 83 units
#>   Within_County: 153 units
#> Phosphorus classification summary:
#>   Excluded: 158 units
#>   Sink_Deficit: 1891 units
#>   Sink_Fertilizer: 372 units
#>   Source: 317 units
#>   Within_County: 320 units
#> Agricultural classification complete!
#> Applied threshold: 1235.53 acres
#> Agricultural classification complete
#>   Spatial units processed:3112
#>   Nitrogen classes:Excluded ( 212 ), Sink_Deficit ( 2450 ), Sink_Fertilizer ( 214 ), Source ( 83 ), Within_County ( 153 )
#>   Phosphorus classes:Excluded ( 212 ), Sink_Deficit ( 1891 ), Sink_Fertilizer ( 372 ), Source ( 317 ), Within_County ( 320 )
#> 
#> Processing WWTP data...
#>   Nutrients:nitrogen
#>   WWTP year:2016
#>   Load units:kg
#>   Data source:Built-in (2016)
#>   Loading built-in nitrogen WWTP data for2016...
#> Using cached version of wwtp_nitrogen_combined
#> Loaded WWTP nitrogen data for year 2016
#> Number of facilities: 20846
#>   Processing nitrogen WWTP facilities...
#> Filtered for positive nitrogen loads:
#>   Original: 20846 facilities
#>   With positive loads: 20846 facilities
#> WWTP nitrogen source classification:
#>   Minor Source: 17801 facilities
#>   Small Source: 1799 facilities
#>   Medium Source: 729 facilities
#>   Large Source: 417 facilities
#>   Very Large Source: 100 facilities
#> Created spatial WWTP data with 20846 facilities
#> Looking for boundary ID column: 'FIPS'
#> Available columns in boundaries: FIPS, County, State_Name, geometry
#> Aggregating WWTP nitrogen loads by spatial boundaries...
#> Aggregation complete:
#>   WWTP facilities: 20846
#>   Spatial units with facilities: 2581
#>   Total nitrogen load: 582738.6 tons/year
#> WWTP data processing complete
#>   nitrogen:20846facilities in2581spatial units
#> 
#> Integrating WWTP and agricultural data...
#> Integrating WWTP nitrogen data with agricultural classifications...
#> Using agricultural ID column: FIPS
#> Combined nitrogen classification summary:
#>   Excluded: 212 units
#>   Sink_Deficit: 2358 units
#>   Sink_Fertilizer: 185 units
#>   Source: 157 units
#>   Within_County: 200 units
#>  Integration complete
#> 
#> Saving results...
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/county_agricultural_2016.rds
#> File size: 1.04 MB
#> Rows: 3112, Columns: 17
#> Geometry type: POLYGON
#> CRS: EPSG:5070
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/county_nitrogen_integrated_2016.rds
#> File size: 1.1 MB
#> Rows: 3112, Columns: 23
#> Geometry type: POLYGON
#> CRS: EPSG:5070
#> Saved centroid data to: /tmp/Rtmp0dSqZ3/county_nitrogen_centroids_2016.csv
#> File size: 760.52 KB
#> Rows: 3112, Columns: 24
#> Longitude range: [-124.158, -67.637]
#> Latitude range: [25.49, 48.826]
#> Saved analysis summary to: /tmp/Rtmp0dSqZ3/analysis_summary_2016.rds
#> Format: RDS
#> File size: 0.7 KB
#>  Results saved to:/tmp/Rtmp0dSqZ3
#>   Files created:4
#> 
#> ======================================================================
#> ANALYSIS COMPLETE
#> ======================================================================
#> Processing time:0.04minutes
#> Scale:county
#> Year:2016
#> Nutrients analyzed:nitrogen
#> Spatial units:3112
#> WWTP facilities:20846
#> Output directory:/tmp/Rtmp0dSqZ3
#> ======================================================================

# Compare scenarios
comparison <- compare_scenarios(list(
  "Base (Agricultural Only)" = base,
  "With WWTP" = wwtp
))
#> Number of scenarios:2
#>   -Base (Agricultural Only)
#>   -With WWTP
#> 
#> Key differences:
#>    scenario delta_sources delta_sinks delta_surplus delta_deficit
#> 1 With WWTP            74        -121      100385.9       -192330
#>   pct_change_sources
#> 1           89.15663

# View comparison data
print(comparison$comparison_data)
#>   n_sources n_sinks n_balanced n_excluded total_surplus_kg total_deficit_kg
#> 1        83    2664          0        212         34200.92          9990394
#> 2       157    2543          0        212        134586.84          9798064
#>   n_sources_ag n_sinks_ag total_surplus_ag_kg total_deficit_ag_kg has_wwtp
#> 1           83       2664            34200.92             9990394    FALSE
#> 2           83       2664            34200.92             9990394     TRUE
#>   total_units  scale year                 scenario
#> 1        3112 county 2016 Base (Agricultural Only)
#> 2        3112 county 2016                With WWTP

# View plots
print(comparison$plots$bar_chart)

# }
```
