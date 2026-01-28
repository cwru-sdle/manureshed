# Batch Analysis Across Multiple Years

Run manureshed analysis across multiple years with consistent parameters

## Usage

``` r
batch_analysis_years(
  years,
  scale = "huc8",
  nutrients = c("nitrogen", "phosphorus"),
  include_wwtp = TRUE,
  output_base_dir = tempdir(),
  create_comparative_plots = TRUE,
  verbose = TRUE,
  ...
)
```

## Arguments

- years:

  Numeric vector. Years to analyze

- scale:

  Character. Spatial scale: "county", "huc8", or "huc2"

- nutrients:

  Character vector. Nutrients to analyze

- include_wwtp:

  Logical. Whether to include WWTP (only available for 2007-2016
  built-in)

- output_base_dir:

  Character. Base output directory

- create_comparative_plots:

  Logical. Whether to create year-over-year comparisons

- verbose:

  Logical. Whether to print progress

- ...:

  Additional arguments passed to run_builtin_analysis

## Value

List of results for each year

## Examples

``` r
# \donttest{
# Analyze trends with WWTP for subset of supported range
batch_results <- batch_analysis_years(
  years = 2010:2012,  # Use smaller range for examples
  scale = "huc8",
  nutrients = "nitrogen",
  include_wwtp = TRUE
)
#> 
#> ======================================================================
#> BATCH MANURESHED ANALYSIS
#> ======================================================================
#> Years:2010-2012(3years)
#> Scale:huc8
#> Nutrients:nitrogen
#> ----------------------------------------------------------------------
#> 
#> Processing year2010...
#> Using cached version of nugis_huc8_data
#> Loaded NuGIS huc8 data for year 2010
#> Number of spatial units: 2111
#> Using cached version of huc8_boundaries
#> Loaded huc8 boundaries
#> Number of spatial units: 2132
#> Using cached version of nugis_county_data
#> Loaded NuGIS county data for year 2010
#> Number of spatial units: 3064
#> Calculated cropland threshold:
#>   County baseline: 500 ha (1235.53 acres)
#>   Percentile in county data: 4.73%
#>   Threshold for target scale: 1506.14 acres
#> Starting complete agricultural classification for huc8 scale...
#> Processed NuGIS data for huc8 scale:
#>   Spatial units: 2111
#>   Converted P2O5 to P using factor: 0.436
#> Nitrogen classification summary:
#>   Excluded: 100 units
#>   Sink_Deficit: 1631 units
#>   Sink_Fertilizer: 215 units
#>   Source: 30 units
#>   Within_Watershed: 135 units
#> Phosphorus classification summary:
#>   Excluded: 100 units
#>   Sink_Deficit: 1191 units
#>   Sink_Fertilizer: 309 units
#>   Source: 206 units
#>   Within_Watershed: 305 units
#> Agricultural classification complete!
#> Applied threshold: 1506.14 acres
#> Using cached version of wwtp_nitrogen_combined
#> Loaded WWTP nitrogen data for year 2010
#> Number of facilities: 24727
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
#> Looking for boundary ID column: 'huc8'
#> Available columns in boundaries: huc8, name, geometry, areasqkm
#> Aggregating WWTP nitrogen loads by spatial boundaries...
#> Aggregation complete:
#>   WWTP facilities: 24727
#>   Spatial units with facilities: 1368
#>   Total nitrogen load: 2009131.37 tons/year
#> Integrating WWTP nitrogen data with agricultural classifications...
#> Using agricultural ID column: huc8
#> Combined nitrogen classification summary:
#>   Excluded: 102 units
#>   Sink_Deficit: 1570 units
#>   Sink_Fertilizer: 198 units
#>   Source: 93 units
#>   Within_Watershed: 169 units
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/year_2010/huc8_agricultural_2010.rds
#> File size: 7.11 MB
#> Rows: 2132, Columns: 17
#> Geometry type: MULTIPOLYGON
#> CRS: EPSG:5070
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/year_2010/huc8_nitrogen_integrated_2010.rds
#> File size: 7.15 MB
#> Rows: 2132, Columns: 23
#> Geometry type: MULTIPOLYGON
#> CRS: EPSG:5070
#> Saved centroid data to: /tmp/Rtmp0dSqZ3/year_2010/huc8_nitrogen_centroids_2010.csv
#> File size: 562.84 KB
#> Rows: 2132, Columns: 24
#> Longitude range: [-124.345, -67.71]
#> Latitude range: [25.201, 48.988]
#> Saved analysis summary to: /tmp/Rtmp0dSqZ3/year_2010/analysis_summary_2010.rds
#> Format: RDS
#> File size: 0.71 KB
#>   Year2010complete (2132 units)
#> Processing year2011...
#> Using cached version of nugis_huc8_data
#> Loaded NuGIS huc8 data for year 2011
#> Number of spatial units: 2111
#> Using cached version of huc8_boundaries
#> Loaded huc8 boundaries
#> Number of spatial units: 2132
#> Using cached version of nugis_county_data
#> Loaded NuGIS county data for year 2011
#> Number of spatial units: 3064
#> Calculated cropland threshold:
#>   County baseline: 500 ha (1235.53 acres)
#>   Percentile in county data: 5.22%
#>   Threshold for target scale: 1547.43 acres
#> Starting complete agricultural classification for huc8 scale...
#> Processed NuGIS data for huc8 scale:
#>   Spatial units: 2111
#>   Converted P2O5 to P using factor: 0.436
#> Nitrogen classification summary:
#>   Excluded: 111 units
#>   Sink_Deficit: 1572 units
#>   Sink_Fertilizer: 264 units
#>   Source: 31 units
#>   Within_Watershed: 133 units
#> Phosphorus classification summary:
#>   Excluded: 111 units
#>   Sink_Deficit: 1037 units
#>   Sink_Fertilizer: 375 units
#>   Source: 213 units
#>   Within_Watershed: 375 units
#> Agricultural classification complete!
#> Applied threshold: 1547.43 acres
#> Using cached version of wwtp_nitrogen_combined
#> Loaded WWTP nitrogen data for year 2011
#> Number of facilities: 25745
#> Filtered for positive nitrogen loads:
#>   Original: 25745 facilities
#>   With positive loads: 25745 facilities
#> WWTP nitrogen source classification:
#>   Minor Source: 20989 facilities
#>   Small Source: 2604 facilities
#>   Medium Source: 1114 facilities
#>   Large Source: 808 facilities
#>   Very Large Source: 230 facilities
#> Created spatial WWTP data with 25745 facilities
#> Looking for boundary ID column: 'huc8'
#> Available columns in boundaries: huc8, name, geometry, areasqkm
#> Aggregating WWTP nitrogen loads by spatial boundaries...
#> Aggregation complete:
#>   WWTP facilities: 25745
#>   Spatial units with facilities: 1397
#>   Total nitrogen load: 1163190.5 tons/year
#> Integrating WWTP nitrogen data with agricultural classifications...
#> Using agricultural ID column: huc8
#> Combined nitrogen classification summary:
#>   Excluded: 113 units
#>   Sink_Deficit: 1501 units
#>   Sink_Fertilizer: 248 units
#>   Source: 95 units
#>   Within_Watershed: 175 units
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/year_2011/huc8_agricultural_2011.rds
#> File size: 7.11 MB
#> Rows: 2132, Columns: 17
#> Geometry type: MULTIPOLYGON
#> CRS: EPSG:5070
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/year_2011/huc8_nitrogen_integrated_2011.rds
#> File size: 7.15 MB
#> Rows: 2132, Columns: 23
#> Geometry type: MULTIPOLYGON
#> CRS: EPSG:5070
#> Saved centroid data to: /tmp/Rtmp0dSqZ3/year_2011/huc8_nitrogen_centroids_2011.csv
#> File size: 564.36 KB
#> Rows: 2132, Columns: 24
#> Longitude range: [-124.345, -67.71]
#> Latitude range: [25.201, 48.988]
#> Saved analysis summary to: /tmp/Rtmp0dSqZ3/year_2011/analysis_summary_2011.rds
#> Format: RDS
#> File size: 0.72 KB
#>   Year2011complete (2132 units)
#> Processing year2012...
#> Using cached version of nugis_huc8_data
#> Loaded NuGIS huc8 data for year 2012
#> Number of spatial units: 2111
#> Using cached version of huc8_boundaries
#> Loaded huc8 boundaries
#> Number of spatial units: 2132
#> Using cached version of nugis_county_data
#> Loaded NuGIS county data for year 2012
#> Number of spatial units: 3064
#> Calculated cropland threshold:
#>   County baseline: 500 ha (1235.53 acres)
#>   Percentile in county data: 5.32%
#>   Threshold for target scale: 1731.65 acres
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
#> Using cached version of wwtp_nitrogen_combined
#> Loaded WWTP nitrogen data for year 2012
#> Number of facilities: 26971
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
#> Integrating WWTP nitrogen data with agricultural classifications...
#> Using agricultural ID column: huc8
#> Combined nitrogen classification summary:
#>   Excluded: 115 units
#>   Sink_Deficit: 1436 units
#>   Sink_Fertilizer: 323 units
#>   Source: 91 units
#>   Within_Watershed: 167 units
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/year_2012/huc8_agricultural_2012.rds
#> File size: 7.11 MB
#> Rows: 2132, Columns: 17
#> Geometry type: MULTIPOLYGON
#> CRS: EPSG:5070
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/year_2012/huc8_nitrogen_integrated_2012.rds
#> File size: 7.15 MB
#> Rows: 2132, Columns: 23
#> Geometry type: MULTIPOLYGON
#> CRS: EPSG:5070
#> Saved centroid data to: /tmp/Rtmp0dSqZ3/year_2012/huc8_nitrogen_centroids_2012.csv
#> File size: 565.05 KB
#> Rows: 2132, Columns: 24
#> Longitude range: [-124.345, -67.71]
#> Latitude range: [25.201, 48.988]
#> Saved analysis summary to: /tmp/Rtmp0dSqZ3/year_2012/analysis_summary_2012.rds
#> Format: RDS
#> File size: 0.72 KB
#>   Year2012complete (2132 units)
#> 
#> Creating comparative visualizations...
#> Saved plot to: /tmp/Rtmp0dSqZ3/trend_nitrogen_2010_2012.png
#> Dimensions: 12 x 8 in at 300 DPI
#> File size: 117.38 KB
#> Device: png
#>   Creatednitrogentrend plot
#> 
#> ======================================================================
#> BATCH ANALYSIS COMPLETE
#> ======================================================================
#> Years processed:3/3
#> Scale:huc8
#> Output directory:/tmp/Rtmp0dSqZ3
#> Comparative plots: Created
#> Batch summary:batch_summary.rds
#> ======================================================================

# Historical analysis without WWTP
historical_results <- batch_analysis_years(
  years = 1990:1992,  # Use smaller range
  scale = "county",
  nutrients = c("nitrogen", "phosphorus"),
  include_wwtp = FALSE
)
#> 
#> ======================================================================
#> BATCH MANURESHED ANALYSIS
#> ======================================================================
#> Years:1990-1992(3years)
#> Scale:county
#> Nutrients:nitrogen, phosphorus
#> ----------------------------------------------------------------------
#> 
#> Processing year1990...
#> Using cached version of nugis_county_data
#> Loaded NuGIS county data for year 1990
#> Number of spatial units: 3064
#> Using cached version of county_boundaries
#> Loaded county boundaries
#> Number of spatial units: 3112
#> Starting complete agricultural classification for county scale...
#> Processed NuGIS data for county scale:
#>   Spatial units: 3064
#>   Converted P2O5 to P using factor: 0.436
#> Nitrogen classification summary:
#>   Excluded: 119 units
#>   Sink_Deficit: 1984 units
#>   Sink_Fertilizer: 674 units
#>   Source: 115 units
#>   Within_County: 172 units
#> Phosphorus classification summary:
#>   Excluded: 119 units
#>   Sink_Deficit: 1060 units
#>   Sink_Fertilizer: 1125 units
#>   Source: 417 units
#>   Within_County: 343 units
#> Agricultural classification complete!
#> Applied threshold: 1235.53 acres
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/year_1990/county_agricultural_1990.rds
#> File size: 1.03 MB
#> Rows: 3112, Columns: 17
#> Geometry type: POLYGON
#> CRS: EPSG:5070
#> Saved analysis summary to: /tmp/Rtmp0dSqZ3/year_1990/analysis_summary_1990.rds
#> Format: RDS
#> File size: 0.5 KB
#>   Year1990complete (3112 units)
#> Processing year1991...
#> Using cached version of nugis_county_data
#> Loaded NuGIS county data for year 1991
#> Number of spatial units: 3064
#> Using cached version of county_boundaries
#> Loaded county boundaries
#> Number of spatial units: 3112
#> Starting complete agricultural classification for county scale...
#> Processed NuGIS data for county scale:
#>   Spatial units: 3064
#>   Converted P2O5 to P using factor: 0.436
#> Nitrogen classification summary:
#>   Excluded: 119 units
#>   Sink_Deficit: 1966 units
#>   Sink_Fertilizer: 649 units
#>   Source: 107 units
#>   Within_County: 223 units
#> Phosphorus classification summary:
#>   Excluded: 119 units
#>   Sink_Deficit: 1041 units
#>   Sink_Fertilizer: 1105 units
#>   Source: 401 units
#>   Within_County: 398 units
#> Agricultural classification complete!
#> Applied threshold: 1235.53 acres
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/year_1991/county_agricultural_1991.rds
#> File size: 1.04 MB
#> Rows: 3112, Columns: 17
#> Geometry type: POLYGON
#> CRS: EPSG:5070
#> Saved analysis summary to: /tmp/Rtmp0dSqZ3/year_1991/analysis_summary_1991.rds
#> Format: RDS
#> File size: 0.5 KB
#>   Year1991complete (3112 units)
#> Processing year1992...
#> Using cached version of nugis_county_data
#> Loaded NuGIS county data for year 1992
#> Number of spatial units: 3064
#> Using cached version of county_boundaries
#> Loaded county boundaries
#> Number of spatial units: 3112
#> Starting complete agricultural classification for county scale...
#> Processed NuGIS data for county scale:
#>   Spatial units: 3064
#>   Converted P2O5 to P using factor: 0.436
#> Nitrogen classification summary:
#>   Excluded: 126 units
#>   Sink_Deficit: 2196 units
#>   Sink_Fertilizer: 445 units
#>   Source: 99 units
#>   Within_County: 198 units
#> Phosphorus classification summary:
#>   Excluded: 126 units
#>   Sink_Deficit: 1221 units
#>   Sink_Fertilizer: 963 units
#>   Source: 380 units
#>   Within_County: 374 units
#> Agricultural classification complete!
#> Applied threshold: 1235.53 acres
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/year_1992/county_agricultural_1992.rds
#> File size: 1.03 MB
#> Rows: 3112, Columns: 17
#> Geometry type: POLYGON
#> CRS: EPSG:5070
#> Saved analysis summary to: /tmp/Rtmp0dSqZ3/year_1992/analysis_summary_1992.rds
#> Format: RDS
#> File size: 0.5 KB
#>   Year1992complete (3112 units)
#> 
#> Creating comparative visualizations...
#> Saved plot to: /tmp/Rtmp0dSqZ3/trend_nitrogen_1990_1992.png
#> Dimensions: 12 x 8 in at 300 DPI
#> File size: 126.69 KB
#> Device: png
#>   Creatednitrogentrend plot
#> Saved plot to: /tmp/Rtmp0dSqZ3/trend_phosphorus_1990_1992.png
#> Dimensions: 12 x 8 in at 300 DPI
#> File size: 142.99 KB
#> Device: png
#>   Createdphosphorustrend plot
#> 
#> ======================================================================
#> BATCH ANALYSIS COMPLETE
#> ======================================================================
#> Years processed:3/3
#> Scale:county
#> Output directory:/tmp/Rtmp0dSqZ3
#> Comparative plots: Created
#> Batch summary:batch_summary.rds
#> ======================================================================

# Mixed analysis: some years with WWTP, some without
mixed_results <- batch_analysis_years(
  years = c(2005, 2010, 2015),  # 2010,2015 will have WWTP
  scale = "huc8",
  nutrients = "nitrogen",
  include_wwtp = TRUE  # Will only apply to 2010,2015
)
#> 
#> ======================================================================
#> BATCH MANURESHED ANALYSIS
#> ======================================================================
#> Years:2005-2015(3years)
#> Scale:huc8
#> Nutrients:nitrogen
#> ----------------------------------------------------------------------
#> 
#> Processing year2005...
#>   Note: WWTP analysis skipped for2005(built-in data only available for 2007-2016)
#> Using cached version of nugis_huc8_data
#> Loaded NuGIS huc8 data for year 2005
#> Number of spatial units: 2111
#> Using cached version of huc8_boundaries
#> Loaded huc8 boundaries
#> Number of spatial units: 2132
#> Using cached version of nugis_county_data
#> Loaded NuGIS county data for year 2005
#> Number of spatial units: 3064
#> Calculated cropland threshold:
#>   County baseline: 500 ha (1235.53 acres)
#>   Percentile in county data: 4.5%
#>   Threshold for target scale: 1214.18 acres
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
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/year_2005/huc8_agricultural_2005.rds
#> File size: 7.11 MB
#> Rows: 2132, Columns: 17
#> Geometry type: MULTIPOLYGON
#> CRS: EPSG:5070
#> Saved analysis summary to: /tmp/Rtmp0dSqZ3/year_2005/analysis_summary_2005.rds
#> Format: RDS
#> File size: 0.52 KB
#>   Year2005complete (2132 units)
#> Processing year2010...
#> Using cached version of nugis_huc8_data
#> Loaded NuGIS huc8 data for year 2010
#> Number of spatial units: 2111
#> Using cached version of huc8_boundaries
#> Loaded huc8 boundaries
#> Number of spatial units: 2132
#> Using cached version of nugis_county_data
#> Loaded NuGIS county data for year 2010
#> Number of spatial units: 3064
#> Calculated cropland threshold:
#>   County baseline: 500 ha (1235.53 acres)
#>   Percentile in county data: 4.73%
#>   Threshold for target scale: 1506.14 acres
#> Starting complete agricultural classification for huc8 scale...
#> Processed NuGIS data for huc8 scale:
#>   Spatial units: 2111
#>   Converted P2O5 to P using factor: 0.436
#> Nitrogen classification summary:
#>   Excluded: 100 units
#>   Sink_Deficit: 1631 units
#>   Sink_Fertilizer: 215 units
#>   Source: 30 units
#>   Within_Watershed: 135 units
#> Phosphorus classification summary:
#>   Excluded: 100 units
#>   Sink_Deficit: 1191 units
#>   Sink_Fertilizer: 309 units
#>   Source: 206 units
#>   Within_Watershed: 305 units
#> Agricultural classification complete!
#> Applied threshold: 1506.14 acres
#> Using cached version of wwtp_nitrogen_combined
#> Loaded WWTP nitrogen data for year 2010
#> Number of facilities: 24727
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
#> Looking for boundary ID column: 'huc8'
#> Available columns in boundaries: huc8, name, geometry, areasqkm
#> Aggregating WWTP nitrogen loads by spatial boundaries...
#> Aggregation complete:
#>   WWTP facilities: 24727
#>   Spatial units with facilities: 1368
#>   Total nitrogen load: 2009131.37 tons/year
#> Integrating WWTP nitrogen data with agricultural classifications...
#> Using agricultural ID column: huc8
#> Combined nitrogen classification summary:
#>   Excluded: 102 units
#>   Sink_Deficit: 1570 units
#>   Sink_Fertilizer: 198 units
#>   Source: 93 units
#>   Within_Watershed: 169 units
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/year_2010/huc8_agricultural_2010.rds
#> File size: 7.11 MB
#> Rows: 2132, Columns: 17
#> Geometry type: MULTIPOLYGON
#> CRS: EPSG:5070
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/year_2010/huc8_nitrogen_integrated_2010.rds
#> File size: 7.15 MB
#> Rows: 2132, Columns: 23
#> Geometry type: MULTIPOLYGON
#> CRS: EPSG:5070
#> Saved centroid data to: /tmp/Rtmp0dSqZ3/year_2010/huc8_nitrogen_centroids_2010.csv
#> File size: 562.84 KB
#> Rows: 2132, Columns: 24
#> Longitude range: [-124.345, -67.71]
#> Latitude range: [25.201, 48.988]
#> Saved analysis summary to: /tmp/Rtmp0dSqZ3/year_2010/analysis_summary_2010.rds
#> Format: RDS
#> File size: 0.72 KB
#>   Year2010complete (2132 units)
#> Processing year2015...
#> Using cached version of nugis_huc8_data
#> Loaded NuGIS huc8 data for year 2015
#> Number of spatial units: 2111
#> Using cached version of huc8_boundaries
#> Loaded huc8 boundaries
#> Number of spatial units: 2132
#> Using cached version of nugis_county_data
#> Loaded NuGIS county data for year 2015
#> Number of spatial units: 3064
#> Calculated cropland threshold:
#>   County baseline: 500 ha (1235.53 acres)
#>   Percentile in county data: 5.32%
#>   Threshold for target scale: 1584.43 acres
#> Starting complete agricultural classification for huc8 scale...
#> Processed NuGIS data for huc8 scale:
#>   Spatial units: 2111
#>   Converted P2O5 to P using factor: 0.436
#> Nitrogen classification summary:
#>   Excluded: 113 units
#>   Sink_Deficit: 1665 units
#>   Sink_Fertilizer: 189 units
#>   Source: 27 units
#>   Within_Watershed: 117 units
#> Phosphorus classification summary:
#>   Excluded: 113 units
#>   Sink_Deficit: 1228 units
#>   Sink_Fertilizer: 271 units
#>   Source: 205 units
#>   Within_Watershed: 294 units
#> Agricultural classification complete!
#> Applied threshold: 1584.43 acres
#> Using cached version of wwtp_nitrogen_combined
#> Loaded WWTP nitrogen data for year 2015
#> Number of facilities: 30394
#> Filtered for positive nitrogen loads:
#>   Original: 30394 facilities
#>   With positive loads: 30394 facilities
#> WWTP nitrogen source classification:
#>   Minor Source: 25261 facilities
#>   Small Source: 2989 facilities
#>   Medium Source: 1154 facilities
#>   Large Source: 812 facilities
#>   Very Large Source: 178 facilities
#> Created spatial WWTP data with 30394 facilities
#> Looking for boundary ID column: 'huc8'
#> Available columns in boundaries: huc8, name, geometry, areasqkm
#> Aggregating WWTP nitrogen loads by spatial boundaries...
#> Aggregation complete:
#>   WWTP facilities: 30394
#>   Spatial units with facilities: 1441
#>   Total nitrogen load: 1141908.76 tons/year
#> Integrating WWTP nitrogen data with agricultural classifications...
#> Using agricultural ID column: huc8
#> Combined nitrogen classification summary:
#>   Excluded: 115 units
#>   Sink_Deficit: 1595 units
#>   Sink_Fertilizer: 170 units
#>   Source: 97 units
#>   Within_Watershed: 155 units
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/year_2015/huc8_agricultural_2015.rds
#> File size: 7.11 MB
#> Rows: 2132, Columns: 17
#> Geometry type: MULTIPOLYGON
#> CRS: EPSG:5070
#> Saved spatial data to: /tmp/Rtmp0dSqZ3/year_2015/huc8_nitrogen_integrated_2015.rds
#> File size: 7.15 MB
#> Rows: 2132, Columns: 23
#> Geometry type: MULTIPOLYGON
#> CRS: EPSG:5070
#> Saved centroid data to: /tmp/Rtmp0dSqZ3/year_2015/huc8_nitrogen_centroids_2015.csv
#> File size: 564.87 KB
#> Rows: 2132, Columns: 24
#> Longitude range: [-124.345, -67.71]
#> Latitude range: [25.201, 48.988]
#> Saved analysis summary to: /tmp/Rtmp0dSqZ3/year_2015/analysis_summary_2015.rds
#> Format: RDS
#> File size: 0.72 KB
#>   Year2015complete (2132 units)
#> 
#> Creating comparative visualizations...
#> Saved plot to: /tmp/Rtmp0dSqZ3/trend_nitrogen_2005_2015.png
#> Dimensions: 12 x 8 in at 300 DPI
#> File size: 115.12 KB
#> Device: png
#>   Creatednitrogentrend plot
#> 
#> ======================================================================
#> BATCH ANALYSIS COMPLETE
#> ======================================================================
#> Years processed:3/3
#> Scale:huc8
#> Output directory:/tmp/Rtmp0dSqZ3
#> Comparative plots: Created
#> Batch summary:batch_summary.rds
#> ======================================================================
# }
```
