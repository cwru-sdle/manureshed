# Complete Manureshed Analysis Workflow (Built-in Data)

Run complete manureshed analysis using built-in NuGIS data (start-2016)
and optional WWTP data. For WWTP analysis beyond 2016, users must
provide their own data. Supports analysis of nitrogen, phosphorus, or
both nutrients simultaneously.

## Usage

``` r
run_builtin_analysis(
  scale = "huc8",
  year = 2016,
  nutrients = c("nitrogen", "phosphorus"),
  output_dir = tempdir(),
  include_wwtp = TRUE,
  wwtp_year = NULL,
  custom_wwtp_nitrogen = NULL,
  custom_wwtp_phosphorus = NULL,
  wwtp_column_mapping = NULL,
  wwtp_skip_rows = 0,
  wwtp_header_row = 1,
  wwtp_load_units = "kg",
  add_texas = FALSE,
  save_outputs = TRUE,
  cropland_threshold = NULL,
  verbose = TRUE
)
```

## Arguments

- scale:

  Character. Spatial scale: "county", "huc8", or "huc2"

- year:

  Numeric. Year to analyze (available: start-2016 for NuGIS, 2016 for
  built-in WWTP)

- nutrients:

  Character vector. Nutrients to analyze: c("nitrogen", "phosphorus") or
  subset

- output_dir:

  Character. Output directory for results (default:
  "manureshed_results")

- include_wwtp:

  Logical. Whether to include WWTP analysis (default: TRUE)

- wwtp_year:

  Numeric. Year for WWTP data (default: same as year, only 2016
  available built-in)

- custom_wwtp_nitrogen:

  Character. Path to custom WWTP nitrogen file (for non-2016 years)

- custom_wwtp_phosphorus:

  Character. Path to custom WWTP phosphorus file (for non-2016 years)

- wwtp_column_mapping:

  Named list. Custom column mapping for WWTP data

- wwtp_skip_rows:

  Numeric. Rows to skip in custom WWTP files (default: 0)

- wwtp_header_row:

  Numeric. Header row in custom WWTP files (default: 1)

- wwtp_load_units:

  Character. Units of WWTP loads: "kg", "lbs", "pounds", "tons"
  (default: "kg")

- add_texas:

  Logical. Whether to add Texas HUC8 data (only for HUC8 scale, default:
  FALSE)

- save_outputs:

  Logical. Whether to save results to files (default: TRUE)

- cropland_threshold:

  Numeric. Custom cropland threshold for exclusion (optional)

- verbose:

  Logical. Whether to print detailed progress messages (default: TRUE)

## Value

List with all analysis results for specified nutrients

## Examples

``` r
# \donttest{
# Basic analysis using built-in data (2007-2016 WWTP available)
results_2016 <- run_builtin_analysis(
  scale = "huc8",
  year = 2016,
  nutrients = c("nitrogen", "phosphorus"),
  include_wwtp = TRUE
)
#> 
#> ======================================================================
#> BATCH MANURESHED ANALYSIS
#> ======================================================================
#> Year: 2016
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
#> Loaded NuGIS huc8 data for year 2016
#> Number of spatial units: 2109
#> Loading built-in spatial boundaries...
#> Using cached version of huc8_boundaries
#> Loaded huc8 boundaries
#> Number of spatial units: 2132
#> Calculating cropland threshold...
#> Using cached version of nugis_county_data
#> Loaded NuGIS county data for year 2016
#> Number of spatial units: 3058
#> Calculated cropland threshold:
#>   County baseline: 500 ha (1235.53 acres)
#>   Percentile in county data: 5.17%
#>   Threshold for target scale: 1452.81 acres
#> Cropland threshold:1452.81acres
#> 
#> Processing agricultural classifications...
#> Starting complete agricultural classification for huc8 scale...
#> Processed NuGIS data for huc8 scale:
#>   Spatial units: 2109
#>   Converted P2O5 to P using factor: 0.436
#> Nitrogen classification summary:
#>   Excluded: 109 units
#>   Sink_Deficit: 1721 units
#>   Sink_Fertilizer: 144 units
#>   Source: 28 units
#>   Within_Watershed: 107 units
#> Phosphorus classification summary:
#>   Excluded: 109 units
#>   Sink_Deficit: 1296 units
#>   Sink_Fertilizer: 217 units
#>   Source: 210 units
#>   Within_Watershed: 277 units
#> Agricultural classification complete!
#> Applied threshold: 1452.81 acres
#> Agricultural classification complete
#>   Spatial units processed:2132
#>   Nitrogen classes:Excluded ( 115 ), Sink_Deficit ( 1734 ), Sink_Fertilizer ( 145 ), Source ( 28 ), Within_Watershed ( 110 )
#>   Phosphorus classes:Excluded ( 115 ), Sink_Deficit ( 1307 ), Sink_Fertilizer ( 219 ), Source ( 211 ), Within_Watershed ( 280 )
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
#> Looking for boundary ID column: 'huc8'
#> Available columns in boundaries: huc8, name, geometry, areasqkm
#> Aggregating WWTP nitrogen loads by spatial boundaries...
#> Aggregation complete:
#>   WWTP facilities: 20846
#>   Spatial units with facilities: 1458
#>   Total nitrogen load: 582759.72 tons/year
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
#> Looking for boundary ID column: 'huc8'
#> Available columns in boundaries: huc8, name, geometry, areasqkm
#> Aggregating WWTP phosphorus loads by spatial boundaries...
#> Aggregation complete:
#>   WWTP facilities: 10148
#>   Spatial units with facilities: 1160
#>   Total phosphorus load: 174715.88 tons/year
#> WWTP data processing complete
#>   nitrogen:20846facilities in1458spatial units
#>   phosphorus:10148facilities in1160spatial units
#> 
#> Integrating WWTP and agricultural data...
#> Integrating WWTP nitrogen data with agricultural classifications...
#> Using agricultural ID column: huc8
#> Combined nitrogen classification summary:
#>   Excluded: 115 units
#>   Sink_Deficit: 1666 units
#>   Sink_Fertilizer: 131 units
#>   Source: 72 units
#>   Within_Watershed: 148 units
#> Integrating WWTP phosphorus data with agricultural classifications...
#> Using agricultural ID column: huc8
#> Combined phosphorus classification summary:
#>   Excluded: 115 units
#>   Sink_Deficit: 1256 units
#>   Sink_Fertilizer: 197 units
#>   Source: 262 units
#>   Within_Watershed: 302 units
#>  Integration complete
#> 
#> Saving results...
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/huc8_agricultural_2016.rds
#> File size: 7.11 MB
#> Rows: 2132, Columns: 17
#> Geometry type: MULTIPOLYGON
#> CRS: EPSG:5070
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/huc8_nitrogen_integrated_2016.rds
#> File size: 7.15 MB
#> Rows: 2132, Columns: 23
#> Geometry type: MULTIPOLYGON
#> CRS: EPSG:5070
#> Saved centroid data to: /tmp/Rtmp0dSqZ3/huc8_nitrogen_centroids_2016.csv
#> File size: 564.95 KB
#> Rows: 2132, Columns: 24
#> Longitude range: [-124.345, -67.71]
#> Latitude range: [25.201, 48.988]
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/huc8_phosphorus_integrated_2016.rds
#> File size: 7.15 MB
#> Rows: 2132, Columns: 23
#> Geometry type: MULTIPOLYGON
#> CRS: EPSG:5070
#> Saved centroid data to: /tmp/Rtmp0dSqZ3/huc8_phosphorus_centroids_2016.csv
#> File size: 554.06 KB
#> Rows: 2132, Columns: 24
#> Longitude range: [-124.345, -67.71]
#> Latitude range: [25.201, 48.988]
#> Saved analysis summary to: /tmp/Rtmp0dSqZ3/analysis_summary_2016.rds
#> Format: RDS
#> File size: 0.78 KB
#>  Results saved to:/tmp/Rtmp0dSqZ3
#>   Files created:6
#> 
#> ======================================================================
#> ANALYSIS COMPLETE
#> ======================================================================
#> Processing time:0.08minutes
#> Scale:huc8
#> Year:2016
#> Nutrients analyzed:nitrogen, phosphorus
#> Spatial units:2132
#> WWTP facilities:30994
#> Output directory:/tmp/Rtmp0dSqZ3
#> ======================================================================

# Analysis for earlier year (no WWTP available) - nitrogen only
results_2010 <- run_builtin_analysis(
  scale = "county",
  year = 2010,
  nutrients = "nitrogen",
  include_wwtp = FALSE
)
#> 
#> ======================================================================
#> BATCH MANURESHED ANALYSIS
#> ======================================================================
#> Year: 2010
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
#> Loaded NuGIS county data for year 2010
#> Number of spatial units: 3064
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
#>   Spatial units: 3064
#>   Converted P2O5 to P using factor: 0.436
#> Nitrogen classification summary:
#>   Excluded: 145 units
#>   Sink_Deficit: 2362 units
#>   Sink_Fertilizer: 287 units
#>   Source: 83 units
#>   Within_County: 187 units
#> Phosphorus classification summary:
#>   Excluded: 145 units
#>   Sink_Deficit: 1760 units
#>   Sink_Fertilizer: 469 units
#>   Source: 343 units
#>   Within_County: 347 units
#> Agricultural classification complete!
#> Applied threshold: 1235.53 acres
#> Agricultural classification complete
#>   Spatial units processed:3112
#>   Nitrogen classes:Excluded ( 193 ), Sink_Deficit ( 2362 ), Sink_Fertilizer ( 287 ), Source ( 83 ), Within_County ( 187 )
#>   Phosphorus classes:Excluded ( 193 ), Sink_Deficit ( 1760 ), Sink_Fertilizer ( 469 ), Source ( 343 ), Within_County ( 347 )
#> 
#> WWTP analysis skipped
#> 
#> Saving results...
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/county_agricultural_2010.rds
#> File size: 1.04 MB
#> Rows: 3112, Columns: 17
#> Geometry type: POLYGON
#> CRS: EPSG:5070
#> Saved analysis summary to: /tmp/Rtmp0dSqZ3/analysis_summary_2010.rds
#> Format: RDS
#> File size: 0.5 KB
#>  Results saved to:/tmp/Rtmp0dSqZ3
#>   Files created:2
#> 
#> ======================================================================
#> ANALYSIS COMPLETE
#> ======================================================================
#> Processing time:0.01minutes
#> Scale:county
#> Year:2010
#> Nutrients analyzed:nitrogen
#> Spatial units:3112
#> Output directory:/tmp/Rtmp0dSqZ3
#> ======================================================================

# Analysis for earlier year with WWTP now available
results_2010 <- run_builtin_analysis(
  scale = "county",
  year = 2010,
  nutrients = "nitrogen",
  include_wwtp = TRUE  # Now supported for 2010!
)
#> 
#> ======================================================================
#> BATCH MANURESHED ANALYSIS
#> ======================================================================
#> Year: 2010
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
#> Loaded NuGIS county data for year 2010
#> Number of spatial units: 3064
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
#>   Spatial units: 3064
#>   Converted P2O5 to P using factor: 0.436
#> Nitrogen classification summary:
#>   Excluded: 145 units
#>   Sink_Deficit: 2362 units
#>   Sink_Fertilizer: 287 units
#>   Source: 83 units
#>   Within_County: 187 units
#> Phosphorus classification summary:
#>   Excluded: 145 units
#>   Sink_Deficit: 1760 units
#>   Sink_Fertilizer: 469 units
#>   Source: 343 units
#>   Within_County: 347 units
#> Agricultural classification complete!
#> Applied threshold: 1235.53 acres
#> Agricultural classification complete
#>   Spatial units processed:3112
#>   Nitrogen classes:Excluded ( 193 ), Sink_Deficit ( 2362 ), Sink_Fertilizer ( 287 ), Source ( 83 ), Within_County ( 187 )
#>   Phosphorus classes:Excluded ( 193 ), Sink_Deficit ( 1760 ), Sink_Fertilizer ( 469 ), Source ( 343 ), Within_County ( 347 )
#> 
#> Processing WWTP data...
#>   Nutrients:nitrogen
#>   WWTP year:2010
#>   Load units:kg
#>   Data source:Built-in (2010)
#>   Loading built-in nitrogen WWTP data for2010...
#> Using cached version of wwtp_nitrogen_combined
#> Loaded WWTP nitrogen data for year 2010
#> Number of facilities: 24727
#>   Processing nitrogen WWTP facilities...
#> Filtered for positive nitrogen loads:
#>   Original: 24727 facilities
#>   With positive loads: 24727 facilities
#> WWTP nitrogen source classification:
#>   Minor Source: 20327 facilities
#>   Small Source: 2445 facilities
#>   Medium Source: 987 facilities
#>   Large Source: 745 facilities
#>   Very Large Source: 223 facilities
#> Created spatial WWTP data with 24727 facilities
#> Looking for boundary ID column: 'FIPS'
#> Available columns in boundaries: FIPS, County, State_Name, geometry
#> Aggregating WWTP nitrogen loads by spatial boundaries...
#> Aggregation complete:
#>   WWTP facilities: 24727
#>   Spatial units with facilities: 2370
#>   Total nitrogen load: 2010631.56 tons/year
#> WWTP data processing complete
#>   nitrogen:24727facilities in2370spatial units
#> 
#> Integrating WWTP and agricultural data...
#> Integrating WWTP nitrogen data with agricultural classifications...
#> Using agricultural ID column: FIPS
#> Combined nitrogen classification summary:
#>   Excluded: 193 units
#>   Sink_Deficit: 2243 units
#>   Sink_Fertilizer: 266 units
#>   Source: 180 units
#>   Within_County: 230 units
#>  Integration complete
#> 
#> Saving results...
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/county_agricultural_2010.rds
#> File size: 1.04 MB
#> Rows: 3112, Columns: 17
#> Geometry type: POLYGON
#> CRS: EPSG:5070
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/county_nitrogen_integrated_2010.rds
#> File size: 1.1 MB
#> Rows: 3112, Columns: 23
#> Geometry type: POLYGON
#> CRS: EPSG:5070
#> Saved centroid data to: /tmp/Rtmp0dSqZ3/county_nitrogen_centroids_2010.csv
#> File size: 752.63 KB
#> Rows: 3112, Columns: 24
#> Longitude range: [-124.158, -67.637]
#> Latitude range: [25.49, 48.826]
#> Saved analysis summary to: /tmp/Rtmp0dSqZ3/analysis_summary_2010.rds
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
#> Year:2010
#> Nutrients analyzed:nitrogen
#> Spatial units:3112
#> WWTP facilities:24727
#> Output directory:/tmp/Rtmp0dSqZ3
#> ======================================================================

# Analysis for year before WWTP availability
results_2005 <- run_builtin_analysis(
  scale = "huc8",
  year = 2005,
  nutrients = "phosphorus",
  include_wwtp = FALSE  # No WWTP data before 2007
)
#> 
#> ======================================================================
#> BATCH MANURESHED ANALYSIS
#> ======================================================================
#> Year: 2005
#> Scale: huc8
#> Nutrients: phosphorus
#> ----------------------------------------------------------------------
#> Checking data availability...
#> Data availability confirmed
#>   Available scales:county, huc8, huc2
#>   Available years forhuc8:1987-2016
#>   Built-in WWTP data:Available (2007-2016)
#> 
#> Loading built-in NuGIS data...
#> Using cached version of nugis_huc8_data
#> Loaded NuGIS huc8 data for year 2005
#> Number of spatial units: 2111
#> Loading built-in spatial boundaries...
#> Using cached version of huc8_boundaries
#> Loaded huc8 boundaries
#> Number of spatial units: 2132
#> Calculating cropland threshold...
#> Using cached version of nugis_county_data
#> Loaded NuGIS county data for year 2005
#> Number of spatial units: 3064
#> Calculated cropland threshold:
#>   County baseline: 500 ha (1235.53 acres)
#>   Percentile in county data: 4.5%
#>   Threshold for target scale: 1214.18 acres
#> Cropland threshold:1214.18acres
#> 
#> Processing agricultural classifications...
#> Starting complete agricultural classification for huc8 scale...
#> Processed NuGIS data for huc8 scale:
#>   Spatial units: 2111
#>   Converted P2O5 to P using factor: 0.436
#> Nitrogen classification summary:
#>   Excluded: 96 units
#>   Sink_Deficit: 1572 units
#>   Sink_Fertilizer: 273 units
#>   Source: 32 units
#>   Within_Watershed: 138 units
#> Phosphorus classification summary:
#>   Excluded: 96 units
#>   Sink_Deficit: 952 units
#>   Sink_Fertilizer: 549 units
#>   Source: 219 units
#>   Within_Watershed: 295 units
#> Agricultural classification complete!
#> Applied threshold: 1214.18 acres
#> Agricultural classification complete
#>   Spatial units processed:2132
#>   Nitrogen classes:Excluded ( 98 ), Sink_Deficit ( 1588 ), Sink_Fertilizer ( 275 ), Source ( 32 ), Within_Watershed ( 139 )
#>   Phosphorus classes:Excluded ( 98 ), Sink_Deficit ( 964 ), Sink_Fertilizer ( 554 ), Source ( 220 ), Within_Watershed ( 296 )
#> 
#> WWTP analysis skipped
#> 
#> Saving results...
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/huc8_agricultural_2005.rds
#> File size: 7.11 MB
#> Rows: 2132, Columns: 17
#> Geometry type: MULTIPOLYGON
#> CRS: EPSG:5070
#> Saved analysis summary to: /tmp/Rtmp0dSqZ3/analysis_summary_2005.rds
#> Format: RDS
#> File size: 0.52 KB
#>  Results saved to:/tmp/Rtmp0dSqZ3
#>   Files created:2
#> 
#> ======================================================================
#> ANALYSIS COMPLETE
#> ======================================================================
#> Processing time:0.02minutes
#> Scale:huc8
#> Year:2005
#> Nutrients analyzed:phosphorus
#> Spatial units:2132
#> Output directory:/tmp/Rtmp0dSqZ3
#> ======================================================================
# }
```
