# Merge multiple raster files into a single raster

Some functions like
[get_tiles](https://docs.ropensci.org/terrainr/reference/get_tiles.md)
return multiple separate files when it can be useful to have a single
larger raster instead. This function is a thin wrapper over
[sf::gdal_utils](https://r-spatial.github.io/sf/reference/gdal_utils.html),
making it easy to collapse those multiple raster files into a single
TIFF.

## Usage

``` r
merge_rasters(
  input_rasters,
  output_raster = tempfile(fileext = ".tif"),
  options = character(0),
  overwrite = FALSE,
  force_fallback = FALSE
)
```

## Arguments

- input_rasters:

  A character vector containing the file paths to the georeferenced
  rasters you want to use.

- output_raster:

  The file path to save the merged georeferenced raster to.

- options:

  Optionally, a character vector of options to be passed directly to
  [sf::gdal_utils](https://r-spatial.github.io/sf/reference/gdal_utils.html).
  If the fallback is used and any options (other than "-overwrite") are
  specified, this will issue a warning.

- overwrite:

  Logical: overwrite `output_raster` if it exists? If FALSE and the file
  exists, this function will fail with an error. The behavior if this
  argument is TRUE and "-overwrite" is passed to `options` directly is
  not stable.

- force_fallback:

  Logical: if TRUE, uses the much slower fallback method by default.
  This is used for testing purposes and is not recommended for use by
  end users.

## Value

`output_raster`, invisibly.

## See also

Other data manipulation functions:
[`combine_overlays()`](https://docs.ropensci.org/terrainr/reference/combine_overlays.md),
[`georeference_overlay()`](https://docs.ropensci.org/terrainr/reference/georeference_overlay.md),
[`raster_to_raw_tiles()`](https://docs.ropensci.org/terrainr/reference/raster_to_raw_tiles.md),
[`vector_to_overlay()`](https://docs.ropensci.org/terrainr/reference/vector_to_overlay.md)

## Examples

``` r
if (FALSE) { # \dontrun{
simulated_data <- data.frame(
  lat = c(44.10379, 44.17573),
  lng = c(-74.01177, -73.91171)
)

simulated_data <- sf::st_as_sf(simulated_data, coords = c("lng", "lat"))

img_files <- get_tiles(simulated_data)
merge_rasters(img_files[[1]])
} # }
```
