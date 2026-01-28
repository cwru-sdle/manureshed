# Print Summary of Analysis Results

Print formatted summary of manureshed analysis results to the console.
The summary includes analysis configuration parameters (scale, year,
nutrients, WWTP inclusion), spatial coverage statistics, agricultural
nutrient classifications with counts and percentages, WWTP integration
metrics (if applicable), integrated classifications (if available),
output file information, and processing time.

## Usage

``` r
summarize_results(results, detailed = FALSE)
```

## Arguments

- results:

  List. Analysis results from
  [`run_builtin_analysis`](https://exelegch.github.io/manureshed-docs/reference/run_builtin_analysis.md)
  or
  [`run_state_analysis`](https://exelegch.github.io/manureshed-docs/reference/run_state_analysis.md).
  Must contain at minimum:

  - `parameters`: List with scale, year, nutrients, include_wwtp

  - `agricultural`: sf data frame with classification columns

  Optional components:

  - `wwtp`: WWTP analysis results

  - `integrated`: Integrated classification results

  - `created_files` or `saved_files`: Output file paths

- detailed:

  Logical. If TRUE, includes additional breakdown of integrated
  classifications showing combined agricultural-WWTP nutrient classes.
  If FALSE (default), shows only agricultural classifications and basic
  WWTP statistics.

## Value

Invisibly returns the input `results` list unchanged. The function is
called primarily for its side effect of printing a formatted summary to
the console. The invisible return allows for piping operations while
displaying the summary.

## Details

The summary output is organized into sections:

- Analysis Configuration:

  Scale, year, nutrients analyzed, WWTP inclusion, state (if applicable)

- Spatial Coverage:

  Total number of spatial units analyzed

- Agricultural Classifications:

  Nitrogen and phosphorus classification counts and percentages

- WWTP Integration:

  Number of facilities and total loads by nutrient (if applicable)

- Integrated Classifications:

  Combined agricultural-WWTP classes (if detailed = TRUE)

- Output Files:

  Number and types of created files (if saved)

- Processing Time:

  Analysis duration in minutes (if available)

Classification names are cleaned for display (underscores replaced with
spaces, line breaks removed). Percentages are rounded to one decimal
place. All console output uses
[`message`](https://rdrr.io/r/base/message.html) and can be suppressed
with [`suppressMessages`](https://rdrr.io/r/base/message.html).

## See also

[`run_builtin_analysis`](https://exelegch.github.io/manureshed-docs/reference/run_builtin_analysis.md)
for generating analysis results,
[`quick_check`](https://exelegch.github.io/manureshed-docs/reference/quick_check.md)
for quick validation,
[`compare_analyses`](https://exelegch.github.io/manureshed-docs/reference/compare_analyses.md)
for comparing two result sets

## Examples

``` r
# \donttest{
# Basic summary
results <- run_builtin_analysis(scale = "county", year = 2016)
#> 
#> ======================================================================
#> BATCH MANURESHED ANALYSIS
#> ======================================================================
#> Year: 2016
#> Scale: county
#> Nutrients: nitrogen, phosphorus
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
#>   Nutrients:nitrogen, phosphorus
#>   WWTP year:2016
#>   Load units:kg
#>   Data source:Built-in (2016)
#>   Loading built-in nitrogen WWTP data for2016...
#> Using cached version of wwtp_nitrogen_combined
#> Loaded WWTP nitrogen data for year 2016
#> Number of facilities: 20846
#>   Loading built-in phosphorus WWTP data for2016...
#> Using cached version of wwtp_phosphorus_combined
#> Loaded WWTP phosphorus data for year 2016
#> Number of facilities: 10148
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
#>   Processing phosphorus WWTP facilities...
#> Filtered for positive phosphorus loads:
#>   Original: 10148 facilities
#>   With positive loads: 10148 facilities
#> WWTP phosphorus source classification:
#>   Minor Source: 6846 facilities
#>   Small Source: 1839 facilities
#>   Medium Source: 795 facilities
#>   Large Source: 561 facilities
#>   Very Large Source: 107 facilities
#> Created spatial WWTP data with 10148 facilities
#> Looking for boundary ID column: 'FIPS'
#> Available columns in boundaries: FIPS, County, State_Name, geometry
#> Aggregating WWTP phosphorus loads by spatial boundaries...
#> Aggregation complete:
#>   WWTP facilities: 10148
#>   Spatial units with facilities: 1966
#>   Total phosphorus load: 177064.66 tons/year
#> WWTP data processing complete
#>   nitrogen:20846facilities in2581spatial units
#>   phosphorus:10148facilities in1966spatial units
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
#> Integrating WWTP phosphorus data with agricultural classifications...
#> Using agricultural ID column: FIPS
#> Combined phosphorus classification summary:
#>   Excluded: 212 units
#>   Sink_Deficit: 1819 units
#>   Sink_Fertilizer: 344 units
#>   Source: 389 units
#>   Within_County: 348 units
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
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/county_phosphorus_integrated_2016.rds
#> File size: 1.09 MB
#> Rows: 3112, Columns: 23
#> Geometry type: POLYGON
#> CRS: EPSG:5070
#> Saved centroid data to: /tmp/Rtmp0dSqZ3/county_phosphorus_centroids_2016.csv
#> File size: 736.85 KB
#> Rows: 3112, Columns: 24
#> Longitude range: [-124.158, -67.637]
#> Latitude range: [25.49, 48.826]
#> Saved analysis summary to: /tmp/Rtmp0dSqZ3/analysis_summary_2016.rds
#> Format: RDS
#> File size: 0.77 KB
#>  Results saved to:/tmp/Rtmp0dSqZ3
#>   Files created:6
#> 
#> ======================================================================
#> ANALYSIS COMPLETE
#> ======================================================================
#> Processing time:0.07minutes
#> Scale:county
#> Year:2016
#> Nutrients analyzed:nitrogen, phosphorus
#> Spatial units:3112
#> WWTP facilities:30994
#> Output directory:/tmp/Rtmp0dSqZ3
#> ======================================================================
summarize_results(results)
#> 
#> ============================================================
#> MANURESHED ANALYSIS SUMMARY
#> ============================================================
#> Analysis Configuration:
#>   Scale:     county
#>   Year:      2016
#>   Nutrients: nitrogen, phosphorus
#>   WWTP:      Yes
#> 
#> Spatial Coverage:
#>   Total units: 3112
#> Agricultural Classifications:
#>   Nitrogen:
#>     excluded               212 (  6.8%)
#>     sink deficit          2450 ( 78.7%)
#>     sink fertilizer        214 (  6.9%)
#>     source                  83 (  2.7%)
#>     within county          153 (  4.9%)
#> 
#>   Phosphorus:
#>     excluded               212 (  6.8%)
#>     sink deficit          1891 ( 60.8%)
#>     sink fertilizer        372 ( 12.0%)
#>     source                 317 ( 10.2%)
#>     within county          320 ( 10.3%)
#> 
#> WWTP Integration:
#>   Nitrogen:
#>     Facilities:  20846
#>     Total load:  634580.1 tons/year
#>   Phosphorus:
#>     Facilities:  10148
#>     Total load:  178423.7 tons/year
#> 
#> Output Files: 4 files created
#> 
#> Processing Time: 0.07 minutes
#> ============================================================

# Detailed summary with integrated classifications
results <- run_builtin_analysis(
  scale = "huc8",
  year = 2012,
  include_wwtp = TRUE
)
#> 
#> ======================================================================
#> BATCH MANURESHED ANALYSIS
#> ======================================================================
#> Year: 2012
#> Scale: huc8
#> Nutrients: nitrogen, phosphorus
#> ----------------------------------------------------------------------
#> Checking data availability...
#> Data availability confirmed
#>   Available scales:county, huc8, huc2
#>   Available years forhuc8:1987-2016
#>   Built-in WWTP data:Available (2007-2016)
#> 
#> Loading built-in NuGIS data...
#> Using cached version of nugis_huc8_data
#> Loaded NuGIS huc8 data for year 2012
#> Number of spatial units: 2111
#> Loading built-in spatial boundaries...
#> Using cached version of huc8_boundaries
#> Loaded huc8 boundaries
#> Number of spatial units: 2132
#> Calculating cropland threshold...
#> Using cached version of nugis_county_data
#> Loaded NuGIS county data for year 2012
#> Number of spatial units: 3064
#> Calculated cropland threshold:
#>   County baseline: 500 ha (1235.53 acres)
#>   Percentile in county data: 5.32%
#>   Threshold for target scale: 1731.65 acres
#> Cropland threshold:1731.65acres
#> 
#> Processing agricultural classifications...
#> Starting complete agricultural classification for huc8 scale...
#> Processed NuGIS data for huc8 scale:
#>   Spatial units: 2111
#>   Converted P2O5 to P using factor: 0.436
#> Nitrogen classification summary:
#>   Excluded: 113 units
#>   Sink_Deficit: 1494 units
#>   Sink_Fertilizer: 340 units
#>   Source: 26 units
#>   Within_Watershed: 138 units
#> Phosphorus classification summary:
#>   Excluded: 113 units
#>   Sink_Deficit: 1073 units
#>   Sink_Fertilizer: 402 units
#>   Source: 197 units
#>   Within_Watershed: 326 units
#> Agricultural classification complete!
#> Applied threshold: 1731.65 acres
#> Agricultural classification complete
#>   Spatial units processed:2132
#>   Nitrogen classes:Excluded ( 115 ), Sink_Deficit ( 1509 ), Sink_Fertilizer ( 342 ), Source ( 26 ), Within_Watershed ( 140 )
#>   Phosphorus classes:Excluded ( 115 ), Sink_Deficit ( 1087 ), Sink_Fertilizer ( 402 ), Source ( 198 ), Within_Watershed ( 330 )
#> 
#> Processing WWTP data...
#>   Nutrients:nitrogen, phosphorus
#>   WWTP year:2012
#>   Load units:kg
#>   Data source:Built-in (2012)
#>   Loading built-in nitrogen WWTP data for2012...
#> Using cached version of wwtp_nitrogen_combined
#> Loaded WWTP nitrogen data for year 2012
#> Number of facilities: 26971
#>   Loading built-in phosphorus WWTP data for2012...
#> Using cached version of wwtp_phosphorus_combined
#> Loaded WWTP phosphorus data for year 2012
#> Number of facilities: 8324
#>   Processing nitrogen WWTP facilities...
#> Filtered for positive nitrogen loads:
#>   Original: 26971 facilities
#>   With positive loads: 26971 facilities
#> WWTP nitrogen source classification:
#>   Minor Source: 22348 facilities
#>   Small Source: 2555 facilities
#>   Medium Source: 1052 facilities
#>   Large Source: 803 facilities
#>   Very Large Source: 213 facilities
#> Created spatial WWTP data with 26971 facilities
#> Looking for boundary ID column: 'huc8'
#> Available columns in boundaries: huc8, name, geometry, areasqkm
#> Aggregating WWTP nitrogen loads by spatial boundaries...
#> Aggregation complete:
#>   WWTP facilities: 26971
#>   Spatial units with facilities: 1403
#>   Total nitrogen load: 1069082.41 tons/year
#>   Processing phosphorus WWTP facilities...
#> Filtered for positive phosphorus loads:
#>   Original: 8324 facilities
#>   With positive loads: 8324 facilities
#> WWTP phosphorus source classification:
#>   Minor Source: 5151 facilities
#>   Small Source: 1680 facilities
#>   Medium Source: 755 facilities
#>   Large Source: 599 facilities
#>   Very Large Source: 139 facilities
#> Created spatial WWTP data with 8324 facilities
#> Looking for boundary ID column: 'huc8'
#> Available columns in boundaries: huc8, name, geometry, areasqkm
#> Aggregating WWTP phosphorus loads by spatial boundaries...
#> Aggregation complete:
#>   WWTP facilities: 8324
#>   Spatial units with facilities: 1004
#>   Total phosphorus load: 86212.84 tons/year
#> WWTP data processing complete
#>   nitrogen:26971facilities in1403spatial units
#>   phosphorus:8324facilities in1004spatial units
#> 
#> Integrating WWTP and agricultural data...
#> Integrating WWTP nitrogen data with agricultural classifications...
#> Using agricultural ID column: huc8
#> Combined nitrogen classification summary:
#>   Excluded: 115 units
#>   Sink_Deficit: 1436 units
#>   Sink_Fertilizer: 323 units
#>   Source: 91 units
#>   Within_Watershed: 167 units
#> Integrating WWTP phosphorus data with agricultural classifications...
#> Using agricultural ID column: huc8
#> Combined phosphorus classification summary:
#>   Excluded: 115 units
#>   Sink_Deficit: 1041 units
#>   Sink_Fertilizer: 381 units
#>   Source: 251 units
#>   Within_Watershed: 344 units
#>  Integration complete
#> 
#> Saving results...
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/huc8_agricultural_2012.rds
#> File size: 7.11 MB
#> Rows: 2132, Columns: 17
#> Geometry type: MULTIPOLYGON
#> CRS: EPSG:5070
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/huc8_nitrogen_integrated_2012.rds
#> File size: 7.15 MB
#> Rows: 2132, Columns: 23
#> Geometry type: MULTIPOLYGON
#> CRS: EPSG:5070
#> Saved centroid data to: /tmp/Rtmp0dSqZ3/huc8_nitrogen_centroids_2012.csv
#> File size: 565.05 KB
#> Rows: 2132, Columns: 24
#> Longitude range: [-124.345, -67.71]
#> Latitude range: [25.201, 48.988]
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/huc8_phosphorus_integrated_2012.rds
#> File size: 7.15 MB
#> Rows: 2132, Columns: 23
#> Geometry type: MULTIPOLYGON
#> CRS: EPSG:5070
#> Saved centroid data to: /tmp/Rtmp0dSqZ3/huc8_phosphorus_centroids_2012.csv
#> File size: 550.58 KB
#> Rows: 2132, Columns: 24
#> Longitude range: [-124.345, -67.71]
#> Latitude range: [25.201, 48.988]
#> Saved analysis summary to: /tmp/Rtmp0dSqZ3/analysis_summary_2012.rds
#> Format: RDS
#> File size: 0.79 KB
#>  Results saved to:/tmp/Rtmp0dSqZ3
#>   Files created:6
#> 
#> ======================================================================
#> ANALYSIS COMPLETE
#> ======================================================================
#> Processing time:0.08minutes
#> Scale:huc8
#> Year:2012
#> Nutrients analyzed:nitrogen, phosphorus
#> Spatial units:2132
#> WWTP facilities:35295
#> Output directory:/tmp/Rtmp0dSqZ3
#> ======================================================================
summarize_results(results, detailed = TRUE)
#> 
#> ============================================================
#> MANURESHED ANALYSIS SUMMARY
#> ============================================================
#> Analysis Configuration:
#>   Scale:     huc8
#>   Year:      2012
#>   Nutrients: nitrogen, phosphorus
#>   WWTP:      Yes
#> 
#> Spatial Coverage:
#>   Total units: 2132
#> Agricultural Classifications:
#>   Nitrogen:
#>     excluded               115 (  5.4%)
#>     sink deficit          1509 ( 70.8%)
#>     sink fertilizer        342 ( 16.0%)
#>     source                  26 (  1.2%)
#>     within watershed       140 (  6.6%)
#> 
#>   Phosphorus:
#>     excluded               115 (  5.4%)
#>     sink deficit          1087 ( 51.0%)
#>     sink fertilizer        402 ( 18.9%)
#>     source                 198 (  9.3%)
#>     within watershed       330 ( 15.5%)
#> 
#> WWTP Integration:
#>   Nitrogen:
#>     Facilities:  26971
#>     Total load:  1163337.0 tons/year
#>   Phosphorus:
#>     Facilities:  8324
#>     Total load:  90409.7 tons/year
#> 
#> Integrated Classifications (with WWTP):
#>   Nitrogen:
#>     excluded               115 (  5.4%)
#>     sink deficit          1436 ( 67.4%)
#>     sink fertilizer        323 ( 15.2%)
#>     source                  91 (  4.3%)
#>     within watershed       167 (  7.8%)
#>   Phosphorus:
#>     excluded               115 (  5.4%)
#>     sink deficit          1041 ( 48.8%)
#>     sink fertilizer        381 ( 17.9%)
#>     source                 251 ( 11.8%)
#>     within watershed       344 ( 16.1%)
#> 
#> Output Files: 4 files created
#>   nitrogen_integrated: huc8_nitrogen_integrated_2012.rds
#>   nitrogen_centroids: huc8_nitrogen_centroids_2012.csv
#>   phosphorus_integrated: huc8_phosphorus_integrated_2012.rds
#>   phosphorus_centroids: huc8_phosphorus_centroids_2012.csv
#> 
#> Processing Time: 0.08 minutes
#> ============================================================
# }
if (FALSE) { # \dontrun{
  # This requires magrittr - never auto-run
  library(magrittr)
  results <- run_builtin_analysis(scale = "huc2", year = 2015) %>%
    summarize_results() %>%
    export_for_gis(output_dir = tempdir())
} # }
```
