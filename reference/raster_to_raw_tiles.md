# Crop a raster and convert the output tiles into new formats.

This function has been deprecated as of terrainr 0.5.0 in favor of the
new function,
[make_manifest](https://docs.ropensci.org/terrainr/reference/unity_crops.md).
While it will be continued to be exported until at least 2022,
improvements and bug fixes will only be made to the new function. Please
open an issue if any features you relied upon is missing from the new
function!

## Usage

``` r
raster_to_raw_tiles(input_file, output_prefix, side_length = 4097, raw = TRUE)
```

## Arguments

- input_file:

  File path to the input TIFF file to convert.

- output_prefix:

  The file path to prefix output tiles with.

- side_length:

  The side length, in pixels, for the .raw tiles.

- raw:

  Logical: Convert the cropped tiles to .raw? When `FALSE` returns a
  .png.

## Value

Invisibly, a character vector containing the file paths that were
written to.

## Details

This function crops input raster files into smaller square tiles and
then converts them into either .png or .raw files which are ready to be
imported into the Unity game engine.

## See also

Other data manipulation functions:
[`combine_overlays()`](https://docs.ropensci.org/terrainr/reference/combine_overlays.md),
[`georeference_overlay()`](https://docs.ropensci.org/terrainr/reference/georeference_overlay.md),
[`merge_rasters()`](https://docs.ropensci.org/terrainr/reference/merge_rasters.md),
[`vector_to_overlay()`](https://docs.ropensci.org/terrainr/reference/vector_to_overlay.md)

Other visualization functions:
[`combine_overlays()`](https://docs.ropensci.org/terrainr/reference/combine_overlays.md),
[`geom_spatial_rgb()`](https://docs.ropensci.org/terrainr/reference/geom_spatial_rgb.md),
[`vector_to_overlay()`](https://docs.ropensci.org/terrainr/reference/vector_to_overlay.md)

## Examples

``` r
if (FALSE) { # \dontrun{
if (!isTRUE(as.logical(Sys.getenv("CI")))) {
  simulated_data <- data.frame(
    id = seq(1, 100, 1),
    lat = runif(100, 44.04905, 44.17609),
    lng = runif(100, -74.01188, -73.83493)
  )
  simulated_data <- sf::st_as_sf(simulated_data, coords = c("lng", "lat"))
  output_files <- get_tiles(simulated_data)
  temptiff <- tempfile(fileext = ".tif")
  merge_rasters(output_files["elevation"][[1]], temptiff)
  raster_to_raw_tiles(temptiff, tempfile())
}
} # }
```
