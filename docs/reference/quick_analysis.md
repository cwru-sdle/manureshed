# Quick Analysis with Visualization

Run analysis and automatically generate key visualizations for specified
nutrients. This is a convenience function that combines
run_builtin_analysis with automatic visualization generation.

## Usage

``` r
quick_analysis(
  scale = "huc8",
  year = 2016,
  nutrients = c("nitrogen", "phosphorus"),
  include_wwtp = TRUE,
  output_dir = tempdir(),
  create_maps = TRUE,
  create_networks = TRUE,
  create_comparisons = TRUE,
  create_wwtp_maps = TRUE,
  wwtp_load_units = "kg",
  map_resolution = "medium",
  generate_report = FALSE,
  verbose = TRUE,
  ...
)
```

## Arguments

- scale:

  Character. Spatial scale: "county", "huc8", or "huc2"

- year:

  Numeric. Year to analyze

- nutrients:

  Character vector. Nutrients to analyze: c("nitrogen", "phosphorus") or
  subset

- include_wwtp:

  Logical. Whether to include WWTP analysis (default: TRUE)

- output_dir:

  Character. Output directory (default: tempdir())

- create_maps:

  Logical. Whether to create classification maps (default: TRUE)

- create_networks:

  Logical. Whether to create network plots (default: TRUE)

- create_comparisons:

  Logical. Whether to create comparison plots (default: TRUE)

- create_wwtp_maps:

  Logical. Whether to create WWTP facility maps (default: TRUE)

- wwtp_load_units:

  Character. Units for WWTP loads if using custom data (default: "kg")

- map_resolution:

  Character. Map resolution: "low", "medium", "high" (default: "medium")

- generate_report:

  Logical. Whether to generate HTML report (default: FALSE)

- verbose:

  Logical. Whether to print progress messages (default: TRUE)

- ...:

  Additional arguments passed to run_builtin_analysis

## Value

List with results and file paths of created visualizations

## Examples

``` r
# \donttest{
# Quick analysis with all visualizations (2007-2016 WWTP available)
results <- quick_analysis(
  scale = "huc8",
  year = 2012,  # Use valid year
  nutrients = c("nitrogen", "phosphorus"),
  include_wwtp = TRUE,
  generate_report = TRUE
)
#> 
#> ======================================================================
#> QUICK MANURESHED ANALYSIS WITH VISUALIZATION
#> ======================================================================
#> Scale:huc8
#> Year:2012
#> Nutrients:nitrogen, phosphorus
#> Visualizations: Maps =TRUE, Networks =TRUE, Comparisons =TRUE
#> ----------------------------------------------------------------------
#> 
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
#> Processing time:0.1minutes
#> Scale:huc8
#> Year:2012
#> Nutrients analyzed:nitrogen, phosphorus
#> Spatial units:2132
#> WWTP facilities:35295
#> Output directory:/tmp/Rtmp0dSqZ3
#> ======================================================================
#> Generating visualizations...
#>   Creatingnitrogenvisualizations...
#> Retrieving data for the year 2024
#>   |                                                                              |                                                                      |   0%  |                                                                              |                                                                      |   1%  |                                                                              |=                                                                     |   1%  |                                                                              |=                                                                     |   2%  |                                                                              |==                                                                    |   2%  |                                                                              |==                                                                    |   3%  |                                                                              |===                                                                   |   4%  |                                                                              |===                                                                   |   5%  |                                                                              |====                                                                  |   5%  |                                                                              |====                                                                  |   6%  |                                                                              |=====                                                                 |   7%  |                                                                              |======                                                                |   8%  |                                                                              |======                                                                |   9%  |                                                                              |=======                                                               |  10%  |                                                                              |========                                                              |  11%  |                                                                              |========                                                              |  12%  |                                                                              |=========                                                             |  13%  |                                                                              |==========                                                            |  14%  |                                                                              |==========                                                            |  15%  |                                                                              |===========                                                           |  15%  |                                                                              |===========                                                           |  16%  |                                                                              |============                                                          |  17%  |                                                                              |=============                                                         |  19%  |                                                                              |==============                                                        |  20%  |                                                                              |===============                                                       |  21%  |                                                                              |================                                                      |  22%  |                                                                              |================                                                      |  23%  |                                                                              |=================                                                     |  24%  |                                                                              |==================                                                    |  25%  |                                                                              |==================                                                    |  26%  |                                                                              |===================                                                   |  27%  |                                                                              |===================                                                   |  28%  |                                                                              |====================                                                  |  29%  |                                                                              |=====================                                                 |  29%  |                                                                              |======================                                                |  31%  |                                                                              |=======================                                               |  32%  |                                                                              |========================                                              |  34%  |                                                                              |========================                                              |  35%  |                                                                              |=========================                                             |  35%  |                                                                              |==========================                                            |  36%  |                                                                              |==========================                                            |  37%  |                                                                              |===========================                                           |  38%  |                                                                              |===========================                                           |  39%  |                                                                              |============================                                          |  39%  |                                                                              |============================                                          |  40%  |                                                                              |============================                                          |  41%  |                                                                              |=============================                                         |  42%  |                                                                              |==============================                                        |  42%  |                                                                              |==============================                                        |  43%  |                                                                              |===============================                                       |  44%  |                                                                              |===============================                                       |  45%  |                                                                              |================================                                      |  45%  |                                                                              |================================                                      |  46%  |                                                                              |=================================                                     |  48%  |                                                                              |==================================                                    |  48%  |                                                                              |===================================                                   |  50%  |                                                                              |====================================                                  |  51%  |                                                                              |====================================                                  |  52%  |                                                                              |=====================================                                 |  52%  |                                                                              |======================================                                |  54%  |                                                                              |=======================================                               |  55%  |                                                                              |========================================                              |  57%  |                                                                              |=========================================                             |  58%  |                                                                              |=========================================                             |  59%  |                                                                              |==========================================                            |  60%  |                                                                              |===========================================                           |  61%  |                                                                              |===========================================                           |  62%  |                                                                              |============================================                          |  63%  |                                                                              |============================================                          |  64%  |                                                                              |==============================================                        |  65%  |                                                                              |==============================================                        |  66%  |                                                                              |===============================================                       |  67%  |                                                                              |================================================                      |  68%  |                                                                              |================================================                      |  69%  |                                                                              |=================================================                     |  70%  |                                                                              |==================================================                    |  71%  |                                                                              |==================================================                    |  72%  |                                                                              |===================================================                   |  73%  |                                                                              |====================================================                  |  74%  |                                                                              |=====================================================                 |  75%  |                                                                              |=====================================================                 |  76%  |                                                                              |======================================================                |  77%  |                                                                              |=======================================================               |  78%  |                                                                              |========================================================              |  79%  |                                                                              |========================================================              |  80%  |                                                                              |=========================================================             |  81%  |                                                                              |=========================================================             |  82%  |                                                                              |==========================================================            |  83%  |                                                                              |==========================================================            |  84%  |                                                                              |===========================================================           |  84%  |                                                                              |============================================================          |  86%  |                                                                              |=============================================================         |  87%  |                                                                              |==============================================================        |  89%  |                                                                              |===============================================================       |  90%  |                                                                              |===============================================================       |  91%  |                                                                              |================================================================      |  91%  |                                                                              |================================================================      |  92%  |                                                                              |=================================================================     |  93%  |                                                                              |==================================================================    |  95%  |                                                                              |===================================================================   |  96%  |                                                                              |====================================================================  |  97%  |                                                                              |===================================================================== |  98%  |                                                                              |===================================================================== |  99%  |                                                                              |======================================================================| 100%
#> Saved plot to: /tmp/Rtmp0dSqZ3/map_agricultural_nitrogen_2012.png
#> Dimensions: 11 x 6 in at 300 DPI
#> File size: 1639.32 KB
#> Device: png
#> Retrieving data for the year 2024
#> Saved plot to: /tmp/Rtmp0dSqZ3/map_combined_nitrogen_2012.png
#> Dimensions: 11 x 6 in at 300 DPI
#> File size: 1646.81 KB
#> Device: png
#> Retrieving data for the year 2024
#> Saved plot to: /tmp/Rtmp0dSqZ3/map_wwtp_influence_nitrogen_2012.png
#> Dimensions: 11 x 6 in at 300 DPI
#> File size: 1689.25 KB
#> Device: png
#> Retrieving data for the year 2024
#> Saved plot to: /tmp/Rtmp0dSqZ3/map_wwtp_facilities_nitrogen_2012.png
#> Dimensions: 11 x 6 in at 300 DPI
#> File size: 1191.16 KB
#> Device: png
#> Created network plot: /tmp/Rtmp0dSqZ3/network_agricultural_nitrogen_2012.png
#> Created network plot: /tmp/Rtmp0dSqZ3/network_combined_nitrogen_2012.png
#> TRANSITION PROBABILITY MATRIX METADATA
#> ======================================
#> 
#> created_date:2026-01-27 20:15:50.752215
#> nutrient:nitrogen
#> analysis_type:agricultural
#> n_categories:4
#> categories:
#>   Sink_Deficit
#>   Sink_Fertilizer
#>   Source
#>   Within_Watershed
#> Saved transition matrix to: /tmp/Rtmp0dSqZ3/transitions_agricultural_nitrogen_2012.csv
#> Saved metadata to: /tmp/Rtmp0dSqZ3/transitions_agricultural_nitrogen_2012_metadata.txt
#> File size: 0.19 KB
#> Matrix dimensions: 4 x 4
#> TRANSITION PROBABILITY MATRIX METADATA
#> ======================================
#> 
#> created_date:2026-01-27 20:15:50.755628
#> nutrient:nitrogen
#> analysis_type:combined
#> n_categories:4
#> categories:
#>   Sink_Deficit
#>   Sink_Fertilizer
#>   Source
#>   Within_Watershed
#> Saved transition matrix to: /tmp/Rtmp0dSqZ3/transitions_combined_nitrogen_2012.csv
#> Saved metadata to: /tmp/Rtmp0dSqZ3/transitions_combined_nitrogen_2012_metadata.txt
#> File size: 0.2 KB
#> Matrix dimensions: 4 x 4
#> Saved plot to: /tmp/Rtmp0dSqZ3/comparison_nitrogen_2012.png
#> Dimensions: 11 x 6 in at 300 DPI
#> File size: 83.44 KB
#> Device: png
#> Saved plot to: /tmp/Rtmp0dSqZ3/impact_nitrogen_2012.png
#> Dimensions: 11 x 6 in at 300 DPI
#> File size: 79.01 KB
#> Device: png
#> Saved plot to: /tmp/Rtmp0dSqZ3/changes_nitrogen_2012.png
#> Dimensions: 11 x 6 in at 300 DPI
#> File size: 81.24 KB
#> Device: png
#>   Creatingphosphorusvisualizations...
#> Retrieving data for the year 2024
#> Saved plot to: /tmp/Rtmp0dSqZ3/map_agricultural_phosphorus_2012.png
#> Dimensions: 11 x 6 in at 300 DPI
#> File size: 1536.55 KB
#> Device: png
#> Retrieving data for the year 2024
#> Saved plot to: /tmp/Rtmp0dSqZ3/map_combined_phosphorus_2012.png
#> Dimensions: 11 x 6 in at 300 DPI
#> File size: 1547.15 KB
#> Device: png
#> Retrieving data for the year 2024
#> Saved plot to: /tmp/Rtmp0dSqZ3/map_wwtp_influence_phosphorus_2012.png
#> Dimensions: 11 x 6 in at 300 DPI
#> File size: 1676.75 KB
#> Device: png
#> Retrieving data for the year 2024
#> Saved plot to: /tmp/Rtmp0dSqZ3/map_wwtp_facilities_phosphorus_2012.png
#> Dimensions: 11 x 6 in at 300 DPI
#> File size: 1248.58 KB
#> Device: png
#> Created network plot: /tmp/Rtmp0dSqZ3/network_agricultural_phosphorus_2012.png
#> Created network plot: /tmp/Rtmp0dSqZ3/network_combined_phosphorus_2012.png
#> TRANSITION PROBABILITY MATRIX METADATA
#> ======================================
#> 
#> created_date:2026-01-27 20:15:57.541814
#> nutrient:phosphorus
#> analysis_type:agricultural
#> n_categories:4
#> categories:
#>   Sink_Deficit
#>   Sink_Fertilizer
#>   Source
#>   Within_Watershed
#> Saved transition matrix to: /tmp/Rtmp0dSqZ3/transitions_agricultural_phosphorus_2012.csv
#> Saved metadata to: /tmp/Rtmp0dSqZ3/transitions_agricultural_phosphorus_2012_metadata.txt
#> File size: 0.2 KB
#> Matrix dimensions: 4 x 4
#> TRANSITION PROBABILITY MATRIX METADATA
#> ======================================
#> 
#> created_date:2026-01-27 20:15:57.545962
#> nutrient:phosphorus
#> analysis_type:combined
#> n_categories:4
#> categories:
#>   Sink_Deficit
#>   Sink_Fertilizer
#>   Source
#>   Within_Watershed
#> Saved transition matrix to: /tmp/Rtmp0dSqZ3/transitions_combined_phosphorus_2012.csv
#> Saved metadata to: /tmp/Rtmp0dSqZ3/transitions_combined_phosphorus_2012_metadata.txt
#> File size: 0.2 KB
#> Matrix dimensions: 4 x 4
#> Saved plot to: /tmp/Rtmp0dSqZ3/comparison_phosphorus_2012.png
#> Dimensions: 11 x 6 in at 300 DPI
#> File size: 84.42 KB
#> Device: png
#> Saved plot to: /tmp/Rtmp0dSqZ3/impact_phosphorus_2012.png
#> Dimensions: 11 x 6 in at 300 DPI
#> File size: 79.21 KB
#> Device: png
#> Saved plot to: /tmp/Rtmp0dSqZ3/changes_phosphorus_2012.png
#> Dimensions: 11 x 6 in at 300 DPI
#> File size: 83.76 KB
#> Device: png
#>   Generating analysis report...
#> Generated analysis report: /tmp/Rtmp0dSqZ3/analysis_report_2012.html
#> Format: HTML
#>  Visualization complete
#>   Files created:25
#>   By type:data_nitrogen ( 1 ), data_phosphorus ( 1 ), facilities_nitrogen_map ( 1 ), facilities_phosphorus_map ( 1 ), influence_nitrogen_map ( 1 ), influence_phosphorus_map ( 1 ), nitrogen ( 3 ), nitrogen_map ( 2 ), nitrogen_network ( 2 ), nitrogen_transitions ( 2 ), phosphorus ( 3 ), phosphorus_map ( 2 ), phosphorus_network ( 2 ), phosphorus_transitions ( 2 ), report ( 1 )
#>   Resolution:medium(11x6 @ 300 DPI)
#>   Total time:0.34minutes
#> 
#> ======================================================================
#> QUICK ANALYSIS COMPLETE
#> ======================================================================
#> Analysis + Visualization time:0.34minutes
#> Output files:29
#> Output directory:/tmp/Rtmp0dSqZ3
#> Nutrients analyzed:nitrogen, phosphorus
#> Report generated:analysis_report_2012.html
#> ======================================================================

# Agricultural only analysis for pre-WWTP year
results <- quick_analysis(
  scale = "county",
  year = 2005,  # Before WWTP data
  nutrients = "nitrogen",
  include_wwtp = FALSE,
  create_networks = FALSE
)
#> 
#> ======================================================================
#> QUICK MANURESHED ANALYSIS WITH VISUALIZATION
#> ======================================================================
#> Scale:county
#> Year:2005
#> Nutrients:nitrogen
#> Visualizations: Maps =TRUE, Networks =FALSE, Comparisons =TRUE
#> ----------------------------------------------------------------------
#> 
#> 
#> ======================================================================
#> BATCH MANURESHED ANALYSIS
#> ======================================================================
#> Year: 2005
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
#> Loaded NuGIS county data for year 2005
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
#>   Excluded: 138 units
#>   Sink_Deficit: 2248 units
#>   Sink_Fertilizer: 408 units
#>   Source: 88 units
#>   Within_County: 182 units
#> Phosphorus classification summary:
#>   Excluded: 138 units
#>   Sink_Deficit: 1410 units
#>   Sink_Fertilizer: 828 units
#>   Source: 372 units
#>   Within_County: 316 units
#> Agricultural classification complete!
#> Applied threshold: 1235.53 acres
#> Agricultural classification complete
#>   Spatial units processed:3112
#>   Nitrogen classes:Excluded ( 186 ), Sink_Deficit ( 2248 ), Sink_Fertilizer ( 408 ), Source ( 88 ), Within_County ( 182 )
#>   Phosphorus classes:Excluded ( 186 ), Sink_Deficit ( 1410 ), Sink_Fertilizer ( 828 ), Source ( 372 ), Within_County ( 316 )
#> 
#> WWTP analysis skipped
#> 
#> Saving results...
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/county_agricultural_2005.rds
#> File size: 1.04 MB
#> Rows: 3112, Columns: 17
#> Geometry type: POLYGON
#> CRS: EPSG:5070
#> Saved analysis summary to: /tmp/Rtmp0dSqZ3/analysis_summary_2005.rds
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
#> Year:2005
#> Nutrients analyzed:nitrogen
#> Spatial units:3112
#> Output directory:/tmp/Rtmp0dSqZ3
#> ======================================================================
#> Generating visualizations...
#>   Creatingnitrogenvisualizations...
#> Retrieving data for the year 2024
#> Saved plot to: /tmp/Rtmp0dSqZ3/map_agricultural_nitrogen_2005.png
#> Dimensions: 11 x 6 in at 300 DPI
#> File size: 1202.14 KB
#> Device: png
#>  Visualization complete
#>   Files created:1
#>   By type:nitrogen_map ( 1 )
#>   Resolution:medium(11x6 @ 300 DPI)
#>   Total time:0.03minutes
#> 
#> ======================================================================
#> QUICK ANALYSIS COMPLETE
#> ======================================================================
#> Analysis + Visualization time:0.03minutes
#> Output files:1
#> Output directory:/tmp/Rtmp0dSqZ3
#> Nutrients analyzed:nitrogen
#> ======================================================================

# High-resolution analysis with expanded year range
results <- quick_analysis(
  scale = "huc8",
  year = 2008,  # Use valid WWTP year
  nutrients = "phosphorus",
  include_wwtp = TRUE,
  map_resolution = "high"
)
#> 
#> ======================================================================
#> QUICK MANURESHED ANALYSIS WITH VISUALIZATION
#> ======================================================================
#> Scale:huc8
#> Year:2008
#> Nutrients:phosphorus
#> Visualizations: Maps =TRUE, Networks =TRUE, Comparisons =TRUE
#> ----------------------------------------------------------------------
#> 
#> 
#> ======================================================================
#> BATCH MANURESHED ANALYSIS
#> ======================================================================
#> Year: 2008
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
#> Loaded NuGIS huc8 data for year 2008
#> Number of spatial units: 2111
#> Loading built-in spatial boundaries...
#> Using cached version of huc8_boundaries
#> Loaded huc8 boundaries
#> Number of spatial units: 2132
#> Calculating cropland threshold...
#> Using cached version of nugis_county_data
#> Loaded NuGIS county data for year 2008
#> Number of spatial units: 3064
#> Calculated cropland threshold:
#>   County baseline: 500 ha (1235.53 acres)
#>   Percentile in county data: 4.44%
#>   Threshold for target scale: 1231.89 acres
#> Cropland threshold:1231.89acres
#> 
#> Processing agricultural classifications...
#> Starting complete agricultural classification for huc8 scale...
#> Processed NuGIS data for huc8 scale:
#>   Spatial units: 2111
#>   Converted P2O5 to P using factor: 0.436
#> Nitrogen classification summary:
#>   Excluded: 94 units
#>   Sink_Deficit: 1635 units
#>   Sink_Fertilizer: 231 units
#>   Source: 34 units
#>   Within_Watershed: 117 units
#> Phosphorus classification summary:
#>   Excluded: 94 units
#>   Sink_Deficit: 1134 units
#>   Sink_Fertilizer: 327 units
#>   Source: 221 units
#>   Within_Watershed: 335 units
#> Agricultural classification complete!
#> Applied threshold: 1231.89 acres
#> Agricultural classification complete
#>   Spatial units processed:2132
#>   Nitrogen classes:Excluded ( 96 ), Sink_Deficit ( 1651 ), Sink_Fertilizer ( 234 ), Source ( 34 ), Within_Watershed ( 117 )
#>   Phosphorus classes:Excluded ( 96 ), Sink_Deficit ( 1147 ), Sink_Fertilizer ( 330 ), Source ( 222 ), Within_Watershed ( 337 )
#> 
#> Processing WWTP data...
#>   Nutrients:phosphorus
#>   WWTP year:2008
#>   Load units:kg
#>   Data source:Built-in (2008)
#>   Loading built-in phosphorus WWTP data for2008...
#> Using cached version of wwtp_phosphorus_combined
#> Loaded WWTP phosphorus data for year 2008
#> Number of facilities: 6838
#>   Processing phosphorus WWTP facilities...
#> Filtered for positive phosphorus loads:
#>   Original: 6838 facilities
#>   With positive loads: 6838 facilities
#> WWTP phosphorus source classification:
#>   Minor Source: 4027 facilities
#>   Small Source: 1473 facilities
#>   Medium Source: 656 facilities
#>   Large Source: 524 facilities
#>   Very Large Source: 158 facilities
#> Created spatial WWTP data with 6838 facilities
#> Looking for boundary ID column: 'huc8'
#> Available columns in boundaries: huc8, name, geometry, areasqkm
#> Aggregating WWTP phosphorus loads by spatial boundaries...
#> Aggregation complete:
#>   WWTP facilities: 6838
#>   Spatial units with facilities: 887
#>   Total phosphorus load: 120477.51 tons/year
#> WWTP data processing complete
#>   phosphorus:6838facilities in887spatial units
#> 
#> Integrating WWTP and agricultural data...
#> Integrating WWTP phosphorus data with agricultural classifications...
#> Using agricultural ID column: huc8
#> Combined phosphorus classification summary:
#>   Excluded: 96 units
#>   Sink_Deficit: 1099 units
#>   Sink_Fertilizer: 304 units
#>   Source: 278 units
#>   Within_Watershed: 355 units
#>  Integration complete
#> 
#> Saving results...
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/huc8_agricultural_2008.rds
#> File size: 7.11 MB
#> Rows: 2132, Columns: 17
#> Geometry type: MULTIPOLYGON
#> CRS: EPSG:5070
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/huc8_phosphorus_integrated_2008.rds
#> File size: 7.14 MB
#> Rows: 2132, Columns: 23
#> Geometry type: MULTIPOLYGON
#> CRS: EPSG:5070
#> Saved centroid data to: /tmp/Rtmp0dSqZ3/huc8_phosphorus_centroids_2008.csv
#> File size: 545.13 KB
#> Rows: 2132, Columns: 24
#> Longitude range: [-124.345, -67.71]
#> Latitude range: [25.201, 48.988]
#> Saved analysis summary to: /tmp/Rtmp0dSqZ3/analysis_summary_2008.rds
#> Format: RDS
#> File size: 0.72 KB
#>  Results saved to:/tmp/Rtmp0dSqZ3
#>   Files created:4
#> 
#> ======================================================================
#> ANALYSIS COMPLETE
#> ======================================================================
#> Processing time:0.04minutes
#> Scale:huc8
#> Year:2008
#> Nutrients analyzed:phosphorus
#> Spatial units:2132
#> WWTP facilities:6838
#> Output directory:/tmp/Rtmp0dSqZ3
#> ======================================================================
#> Generating visualizations...
#>   Creatingphosphorusvisualizations...
#> Retrieving data for the year 2024
#> Saved plot to: /tmp/Rtmp0dSqZ3/map_agricultural_phosphorus_2008.png
#> Dimensions: 16 x 9 in at 450 DPI
#> File size: 4582.24 KB
#> Device: png
#> Retrieving data for the year 2024
#> Saved plot to: /tmp/Rtmp0dSqZ3/map_combined_phosphorus_2008.png
#> Dimensions: 16 x 9 in at 450 DPI
#> File size: 4606.45 KB
#> Device: png
#> Retrieving data for the year 2024
#> Saved plot to: /tmp/Rtmp0dSqZ3/map_wwtp_influence_phosphorus_2008.png
#> Dimensions: 16 x 9 in at 450 DPI
#> File size: 5047.38 KB
#> Device: png
#> Retrieving data for the year 2024
#> Saved plot to: /tmp/Rtmp0dSqZ3/map_wwtp_facilities_phosphorus_2008.png
#> Dimensions: 16 x 9 in at 450 DPI
#> File size: 3454.32 KB
#> Device: png
#> Created network plot: /tmp/Rtmp0dSqZ3/network_agricultural_phosphorus_2008.png
#> Created network plot: /tmp/Rtmp0dSqZ3/network_combined_phosphorus_2008.png
#> TRANSITION PROBABILITY MATRIX METADATA
#> ======================================
#> 
#> created_date:2026-01-27 20:16:11.08319
#> nutrient:phosphorus
#> analysis_type:agricultural
#> n_categories:4
#> categories:
#>   Sink_Deficit
#>   Sink_Fertilizer
#>   Source
#>   Within_Watershed
#> Saved transition matrix to: /tmp/Rtmp0dSqZ3/transitions_agricultural_phosphorus_2008.csv
#> Saved metadata to: /tmp/Rtmp0dSqZ3/transitions_agricultural_phosphorus_2008_metadata.txt
#> File size: 0.2 KB
#> Matrix dimensions: 4 x 4
#> TRANSITION PROBABILITY MATRIX METADATA
#> ======================================
#> 
#> created_date:2026-01-27 20:16:11.086663
#> nutrient:phosphorus
#> analysis_type:combined
#> n_categories:4
#> categories:
#>   Sink_Deficit
#>   Sink_Fertilizer
#>   Source
#>   Within_Watershed
#> Saved transition matrix to: /tmp/Rtmp0dSqZ3/transitions_combined_phosphorus_2008.csv
#> Saved metadata to: /tmp/Rtmp0dSqZ3/transitions_combined_phosphorus_2008_metadata.txt
#> File size: 0.2 KB
#> Matrix dimensions: 4 x 4
#> Saved plot to: /tmp/Rtmp0dSqZ3/comparison_phosphorus_2008.png
#> Dimensions: 16 x 9 in at 450 DPI
#> File size: 190.9 KB
#> Device: png
#> Saved plot to: /tmp/Rtmp0dSqZ3/impact_phosphorus_2008.png
#> Dimensions: 16 x 9 in at 450 DPI
#> File size: 185.55 KB
#> Device: png
#> Saved plot to: /tmp/Rtmp0dSqZ3/changes_phosphorus_2008.png
#> Dimensions: 16 x 9 in at 450 DPI
#> File size: 190.03 KB
#> Device: png
#>  Visualization complete
#>   Files created:12
#>   By type:data_phosphorus ( 1 ), facilities_phosphorus_map ( 1 ), influence_phosphorus_map ( 1 ), phosphorus ( 3 ), phosphorus_map ( 2 ), phosphorus_network ( 2 ), phosphorus_transitions ( 2 )
#>   Resolution:high(16x9 @ 450 DPI)
#>   Total time:0.22minutes
#> 
#> ======================================================================
#> QUICK ANALYSIS COMPLETE
#> ======================================================================
#> Analysis + Visualization time:0.22minutes
#> Output files:14
#> Output directory:/tmp/Rtmp0dSqZ3
#> Nutrients analyzed:phosphorus
#> ======================================================================
# }
```
