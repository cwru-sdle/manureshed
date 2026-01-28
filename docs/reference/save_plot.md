# Save Plot

Save ggplot object to file with publication-quality settings

## Usage

``` r
save_plot(
  plot,
  file_path,
  width = 11,
  height = 6,
  dpi = 300,
  units = "in",
  device = NULL
)
```

## Arguments

- plot:

  ggplot object. Plot to save

- file_path:

  Character. Output file path

- width:

  Numeric. Plot width in inches (default: 11)

- height:

  Numeric. Plot height in inches (default: 6)

- dpi:

  Numeric. Resolution in dots per inch (default: 300)

- units:

  Character. Units for width and height (default: "in")

- device:

  Character. Output device (auto-detected from file extension)

## Value

Character. Path to saved file

## Examples

``` r
# \donttest{
# Create a simple plot for demonstration
library(ggplot2)
p <- ggplot(mtcars, aes(x = mpg, y = hp)) + geom_point()

# Save with default settings (300 DPI, 11x6 inches)
save_plot(p, file.path(tempdir(), "test_plot.png"))
#> Saved plot to: /tmp/Rtmp0dSqZ3/test_plot.png
#> Dimensions: 11 x 6 in at 300 DPI
#> File size: 50.33 KB
#> Device: png
#> [1] "/tmp/Rtmp0dSqZ3/test_plot.png"

# Save with custom dimensions for presentation
save_plot(p, file.path(tempdir(), "presentation_plot.png"), width = 16, height = 9)
#> Saved plot to: /tmp/Rtmp0dSqZ3/presentation_plot.png
#> Dimensions: 16 x 9 in at 300 DPI
#> File size: 72.17 KB
#> Device: png
#> [1] "/tmp/Rtmp0dSqZ3/presentation_plot.png"

# Save as PDF for publication
save_plot(p, file.path(tempdir(), "publication_figure.pdf"), width = 8, height = 6)
#> Saved plot to: /tmp/Rtmp0dSqZ3/publication_figure.pdf
#> Dimensions: 8 x 6 in at 300 DPI
#> File size: 6.25 KB
#> Device: pdf
#> [1] "/tmp/Rtmp0dSqZ3/publication_figure.pdf"
# }
```
