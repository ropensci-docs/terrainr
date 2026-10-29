# Combine multiple image overlays into a single file

This function combines any number of images into a single file, which
may then be further processed as an image or transformed into an image
overlay.

## Usage

``` r
combine_overlays(
  ...,
  output_file = tempfile(fileext = ".png"),
  transparency = 0
)
```

## Arguments

- ...:

  File paths for images to be combined. Note that combining TIFF images
  requires the `tiff` package be installed.

- output_file:

  The path to save the resulting image to. Can be any format accepted by
  [magick::image_read](https://docs.ropensci.org/magick/reference/editing.html).
  Optionally, can be set to `NULL`, in which case this function will
  return the image as a `magick` object instead of writing to disk.

- transparency:

  A value indicating how much transparency should be added to each
  image. If less than 1, interpreted as a proportion (so a value of 0.1
  results in each image becoming 10% more transparent); if between 1 and
  100, interpreted as a percentage (so a value of 10 results in each
  image becoming 10% more transparent.) A value of 0 is equivalent to no
  additional transparency.

## Value

If `output_file` is not null, `output_file`, invisibly. If `output_file`
is null, a `magick` image object.

## See also

Other data manipulation functions:
[`georeference_overlay()`](https://docs.ropensci.org/terrainr/reference/georeference_overlay.md),
[`merge_rasters()`](https://docs.ropensci.org/terrainr/reference/merge_rasters.md),
[`raster_to_raw_tiles()`](https://docs.ropensci.org/terrainr/reference/raster_to_raw_tiles.md),
[`vector_to_overlay()`](https://docs.ropensci.org/terrainr/reference/vector_to_overlay.md)

Other overlay creation functions:
[`georeference_overlay()`](https://docs.ropensci.org/terrainr/reference/georeference_overlay.md),
[`vector_to_overlay()`](https://docs.ropensci.org/terrainr/reference/vector_to_overlay.md)

Other visualization functions:
[`geom_spatial_rgb()`](https://docs.ropensci.org/terrainr/reference/geom_spatial_rgb.md),
[`raster_to_raw_tiles()`](https://docs.ropensci.org/terrainr/reference/raster_to_raw_tiles.md),
[`vector_to_overlay()`](https://docs.ropensci.org/terrainr/reference/vector_to_overlay.md)

## Examples

``` r
if (FALSE) { # \dontrun{
# Generate points and download orthoimagery
mt_elbert_points <- data.frame(
  lat = runif(100, min = 39.11144, max = 39.12416),
  lng = runif(100, min = -106.4534, max = -106.437)
)

mt_elbert_sf <- sf::st_as_sf(mt_elbert_points, coords = c("lng", "lat"))
sf::st_crs(mt_elbert_sf) <- sf::st_crs(4326)

output_files <- get_tiles(
  mt_elbert_sf,
  output_prefix = tempfile(),
  services = c("ortho")
)

# Merge orthoimagery into a single file
ortho_merged <- merge_rasters(
  input_rasters = output_files[1],
  output_raster = tempfile(fileext = ".tif")
)

# Convert our points into an overlay
mt_elbert_overlay <- vector_to_overlay(mt_elbert_sf,
  ortho_merged[[1]],
  size = 15,
  color = "red",
  na.rm = TRUE
)

# Combine the overlay with our orthoimage
ortho_with_points <- combine_overlays(
  ortho_merged[[1]],
  mt_elbert_overlay
)
} # }
```
