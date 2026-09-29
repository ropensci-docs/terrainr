# Georeference image overlays based on a reference raster

This function georeferences an image overlay based on a reference
raster, setting the extent and CRS of the image to those of the raster
file. To georeference multiple images and merge them into a single file,
see
[merge_rasters](https://docs.ropensci.org/terrainr/reference/merge_rasters.md).

## Usage

``` r
georeference_overlay(
  overlay_file,
  reference_raster,
  output_file = tempfile(fileext = ".tif")
)
```

## Arguments

- overlay_file:

  The image overlay to georeference. File format will be detected
  automatically from file extension; options include `jpeg/jpg`, `png`,
  and `tif/tiff`.

- reference_raster:

  The raster file to base georeferencing on. The output image will have
  the same extent and CRS as the reference raster. Accepts anything that
  can be read by
  [terra::rast](https://rspatial.github.io/terra/reference/rast.html)

- output_file:

  The path to write the georeferenced image file to. Must be a TIFF.

## Value

The file path written to, invisibly.

## See also

Other data manipulation functions:
[`combine_overlays()`](https://docs.ropensci.org/terrainr/reference/combine_overlays.md),
[`merge_rasters()`](https://docs.ropensci.org/terrainr/reference/merge_rasters.md),
[`raster_to_raw_tiles()`](https://docs.ropensci.org/terrainr/reference/raster_to_raw_tiles.md),
[`vector_to_overlay()`](https://docs.ropensci.org/terrainr/reference/vector_to_overlay.md)

Other overlay creation functions:
[`combine_overlays()`](https://docs.ropensci.org/terrainr/reference/combine_overlays.md),
[`vector_to_overlay()`](https://docs.ropensci.org/terrainr/reference/vector_to_overlay.md)

## Examples

``` r
if (FALSE) { # \dontrun{
simulated_data <- data.frame(
  id = seq(1, 100, 1),
  lat = runif(100, 44.1114, 44.1123),
  lng = runif(100, -73.92273, -73.92147)
)

simulated_data <- sf::st_as_sf(simulated_data, coords = c("lng", "lat"))

downloaded_tiles <- get_tiles(simulated_data,
  services = c("elevation", "ortho"),
  georeference = FALSE
)

georeference_overlay(
  overlay_file = downloaded_tiles[[2]],
  reference_raster = downloaded_tiles[[1]],
  output_file = tempfile(fileext = ".tif")
)
} # }
```
