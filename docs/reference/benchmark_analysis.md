# Benchmark Analysis Performance

Test analysis speed and memory usage

## Usage

``` r
benchmark_analysis(
  scale = "huc8",
  year = 2016,
  nutrients = "nitrogen",
  n_runs = 3,
  include_wwtp = TRUE
)
```

## Arguments

- scale:

  Character. Spatial scale

- year:

  Numeric. Year to test

- nutrients:

  Character vector. Nutrients to analyze

- n_runs:

  Integer. Number of benchmark runs (default: 3)

- include_wwtp:

  Logical. Include WWTP processing

## Value

List with timing statistics and memory usage

## Examples

``` r
# \donttest{
# Benchmark HUC8 analysis - use smaller scale for faster testing
benchmark <- benchmark_analysis(
  scale = "county",  # Use county for faster testing
  year = 2016,
  nutrients = "nitrogen",
  n_runs = 2  # Reduce runs for faster testing
)
#> Benchmarking analysis performance...
#>   Scale: county
#>   Year: 2016
#>   Runs: 2
#> 
#> Run 1/2
#> Using cached version of nugis_county_data
#> Loaded NuGIS county data for year 2016
#> Number of spatial units: 3058
#> Using cached version of county_boundaries
#> Loaded county boundaries
#> Number of spatial units: 3112
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
#> Using cached version of wwtp_nitrogen_combined
#> Loaded WWTP nitrogen data for year 2016
#> Number of facilities: 20846
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
#> Integrating WWTP nitrogen data with agricultural classifications...
#> Using agricultural ID column: FIPS
#> Combined nitrogen classification summary:
#>   Excluded: 212 units
#>   Sink_Deficit: 2358 units
#>   Sink_Fertilizer: 185 units
#>   Source: 157 units
#>   Within_County: 200 units
#> 
#> Run 2/2
#> Using cached version of nugis_county_data
#> Loaded NuGIS county data for year 2016
#> Number of spatial units: 3058
#> Using cached version of county_boundaries
#> Loaded county boundaries
#> Number of spatial units: 3112
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
#> Using cached version of wwtp_nitrogen_combined
#> Loaded WWTP nitrogen data for year 2016
#> Number of facilities: 20846
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
#> Integrating WWTP nitrogen data with agricultural classifications...
#> Using agricultural ID column: FIPS
#> Combined nitrogen classification summary:
#>   Excluded: 212 units
#>   Sink_Deficit: 2358 units
#>   Sink_Fertilizer: 185 units
#>   Source: 157 units
#>   Within_County: 200 units
print(benchmark)
#> $scale
#> [1] "county"
#> 
#> $year
#> [1] 2016
#> 
#> $nutrients
#> [1] "nitrogen"
#> 
#> $include_wwtp
#> [1] TRUE
#> 
#> $n_runs
#> [1] 2
#> 
#> $timing
#> $timing$mean
#> [1] 2.327268
#> 
#> $timing$sd
#> [1] 0.0480206
#> 
#> $timing$min
#> [1] 2.293313
#> 
#> $timing$max
#> [1] 2.361224
#> 
#> $timing$median
#> [1] 2.327268
#> 
#> $timing$all_runs
#> [1] 2.361224 2.293313
#> 
#> 
#> $memory_mb
#> $memory_mb$mean
#> [1] 11.8
#> 
#> $memory_mb$max
#> [1] 11.8
#> 
#> $memory_mb$all_runs
#> [1] 11.8 11.8
#> 
#> 
#> $timestamp
#> [1] "2026-01-27 20:14:51 EST"
#> 
#> attr(,"class")
#> [1] "manureshed_benchmark" "list"                
# }
```
