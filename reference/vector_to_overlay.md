# Turn spatial vector data into an image overlay

This function allows users to quickly transform any vector data into an
image overlay, which may then be imported as a texture into Unity.

## Usage

``` r
vector_to_overlay(
  vector_data,
  reference_raster,
  output_file = NULL,
  transparent = "#ffffff",
  ...,
  error_crs = NULL
)
```

## Arguments

- vector_data:

  The spatial vector data set to be transformed into an overlay image.
  Users may provide either an `sf` object or a length 1 character vector
  containing a path to a file readable by
  [sf::read_sf](https://r-spatial.github.io/sf/reference/st_read.html).

- reference_raster:

  The raster file to produce an overlay for. The output overlay will
  have the same extent and resolution as the input raster. Users may
  provide either a Raster\* object or a length 1 character vector
  containing a path to a file readable by
  [terra::rast](https://rspatial.github.io/terra/reference/rast.html).

- output_file:

  The path to save the image overlay to. If `NULL`, saves to a tempfile.

- transparent:

  The hex code for a color to be made transparent in the final image.
  Set to `FALSE` to not set any colors to transparent.

- ...:

  Arguments passed to `...` in either
  [ggplot2::geom_point](https://ggplot2.tidyverse.org/reference/geom_point.html)
  (for point vector data),
  [ggplot2::geom_line](https://ggplot2.tidyverse.org/reference/geom_path.html)
  (for line data), or
  [ggplot2::geom_polygon](https://ggplot2.tidyverse.org/reference/geom_polygon.html)
  (for all other data types).

- error_crs:

  Logical: Should this function error if `data` has no CRS? If `TRUE`,
  function errors; if `FALSE`, function quietly assumes EPSG:4326. If
  `NULL`, the default, function assumes EPSG:4326 with a warning.

## Value

`output_file`, invisibly.

## See also

Other data manipulation functions:
[`combine_overlays()`](https://docs.ropensci.org/terrainr/reference/combine_overlays.md),
[`georeference_overlay()`](https://docs.ropensci.org/terrainr/reference/georeference_overlay.md),
[`merge_rasters()`](https://docs.ropensci.org/terrainr/reference/merge_rasters.md),
[`raster_to_raw_tiles()`](https://docs.ropensci.org/terrainr/reference/raster_to_raw_tiles.md)

Other overlay creation functions:
[`combine_overlays()`](https://docs.ropensci.org/terrainr/reference/combine_overlays.md),
[`georeference_overlay()`](https://docs.ropensci.org/terrainr/reference/georeference_overlay.md)

Other visualization functions:
[`combine_overlays()`](https://docs.ropensci.org/terrainr/reference/combine_overlays.md),
[`geom_spatial_rgb()`](https://docs.ropensci.org/terrainr/reference/geom_spatial_rgb.md),
[`raster_to_raw_tiles()`](https://docs.ropensci.org/terrainr/reference/raster_to_raw_tiles.md)

## Examples

``` r
if (FALSE) { # \dontrun{

# Generate points to download raster tiles for
set.seed(123)
simulated_data <- data.frame(
  id = seq(1, 100, 1),
  lat = runif(100, 44.1114, 44.1123),
  lng = runif(100, -73.92273, -73.92147)
)

# Create an sf object from our original simulated data

simulated_data_sf <- sf::st_as_sf(simulated_data, coords = c("lng", "lat"))
sf::st_crs(simulated_data_sf) <- sf::st_crs(4326)

# Download data!

downloaded_tiles <- get_tiles(simulated_data_sf, tempfile())

merged_file <- merge_rasters(
  downloaded_tiles[[1]],
  tempfile(fileext = ".tif")
)


# Create an overlay image
vector_to_overlay(simulated_data_sf, merged_file[[1]], na.rm = TRUE)
} # }
```
